# Telescope Target Types

> **Supported analysis targets and preparation logic**

## Supported Targets

### 1. Local Path

**Format:**
```bash
/path/to/project
./relative/path
~/home/path
C:\Windows\Path
```

**Detection:**
- No URL schema (http://, https://)
- Contains path separators (/, \)
- May start with ., ~, /, or drive letter

**Preparation:**
```bash
1. Validate path exists
   if not exists(path):
     error: "Path does not exist: {path}"

2. Set target_path = path

3. Extract project_name:
   project_name = basename(path)
   # Example: "/Users/ktrua/projects/myapp" → "myapp"

4. Set target_type = "local_path"

5. No cleanup needed (analyzing in place)
```

**Example:**
```yaml
Input: "/Users/ktrua/source/polygon"
Output:
  target_type: "local_path"
  target_path: "/Users/ktrua/source/polygon"
  project_name: "polygon"
  temp_dir: null
  cleanup_required: false
```

---

### 2. GitHub Repository

**Format:**
```bash
https://github.com/user/repo
https://github.com/user/repo.git
git@github.com:user/repo.git
https://github.com/user/repo@branch
https://github.com/user/repo@v1.0
```

**Detection:**
- Contains "github.com"
- May include .git extension
- May include @branch or @tag

**Preparation:**
```bash
1. Parse URL:
   host = "github.com"
   user = extract_user(url)
   repo = extract_repo(url)
   branch = extract_branch(url)  # if @branch specified

2. Create temp directory:
   timestamp = unix_timestamp()
   temp_dir = "/tmp/telescope-{repo}-{timestamp}"

3. Clone repository:
   if branch:
     git clone -b {branch} {url} {temp_dir}
   else:
     git clone {url} {temp_dir}

4. Remove .git directory:
   rm -rf {temp_dir}/.git
   # Reason: Clean snapshot, no git history in analysis

5. Set variables:
   target_path = temp_dir
   project_name = repo
   target_type = "github"

6. Cleanup required: true
```

**Example:**
```yaml
Input: "https://github.com/anthropics/agent-starter-pack"
Output:
  target_type: "github"
  target_path: "/tmp/telescope-agent-starter-pack-1696789234"
  project_name: "agent-starter-pack"
  temp_dir: "/tmp/telescope-agent-starter-pack-1696789234"
  cleanup_required: true
  original_url: "https://github.com/anthropics/agent-starter-pack"
```

---

### 3. GitLab Repository

**Format:**
```bash
https://gitlab.com/user/repo
https://gitlab.com/group/subgroup/repo
git@gitlab.com:user/repo.git
```

**Detection:**
- Contains "gitlab.com"

**Preparation:**
```bash
# Same as GitHub, but:
target_type = "gitlab"
```

---

### 4. Bitbucket Repository

**Format:**
```bash
https://bitbucket.org/user/repo
git@bitbucket.org:user/repo.git
```

**Detection:**
- Contains "bitbucket.org"

**Preparation:**
```bash
# Same as GitHub, but:
target_type = "bitbucket"
```

---

## Target Validation

### Before Analysis Begins

**For Local Paths:**
```python
def validate_local_path(path: str) -> bool:
    """Validate local path exists and is accessible."""
    if not os.path.exists(path):
        raise ValueError(f"Path does not exist: {path}")

    if not os.path.isdir(path):
        raise ValueError(f"Path is not a directory: {path}")

    if not os.access(path, os.R_OK):
        raise ValueError(f"No read permission for path: {path}")

    return True
```

**For Remote URLs:**
```python
def validate_remote_url(url: str) -> bool:
    """Validate remote URL is accessible."""
    # Check URL format
    if not url.startswith(('http://', 'https://', 'git@')):
        raise ValueError(f"Invalid URL format: {url}")

    # Check host is supported
    supported_hosts = ['github.com', 'gitlab.com', 'bitbucket.org']
    if not any(host in url for host in supported_hosts):
        raise ValueError(f"Unsupported repository host: {url}")

    return True
```

---

## Project Name Extraction

### From Local Path

```python
def extract_project_name_from_path(path: str) -> str:
    """Extract project name from local path."""
    # Get basename
    name = os.path.basename(os.path.abspath(path))

    # Clean up name
    name = name.replace(' ', '-').lower()

    return name

# Examples:
# "/Users/ktrua/source/MyApp" → "myapp"
# "/home/user/projects/my-project" → "my-project"
# "C:\Projects\App Name" → "app-name"
```

### From Remote URL

```python
def extract_project_name_from_url(url: str) -> str:
    """Extract project name from repository URL."""
    # Remove .git extension
    url = url.replace('.git', '')

    # Extract repo name (last part of path)
    parts = url.rstrip('/').split('/')
    name = parts[-1]

    # Remove branch/tag if present
    if '@' in name:
        name = name.split('@')[0]

    return name.lower()

# Examples:
# "https://github.com/user/MyRepo" → "myrepo"
# "https://github.com/user/repo.git" → "repo"
# "https://github.com/user/repo@v1.0" → "repo"
```

### Custom Name Override

```bash
User: "Telescope analyze /path/to/project as CustomName"

Logic:
  if "as" in command:
    project_name = extract_after_as(command)
  else:
    project_name = extract_from_target(target)
```

---

## Cleanup Logic

### After Analysis Complete

**For Remote Clones:**
```bash
# In Phase 6 (Cleanup)
if cleanup_required:
  if os.path.exists(temp_dir):
    shutil.rmtree(temp_dir)
    log(f"Cleaned temporary directory: {temp_dir}")
```

**For Local Paths:**
```bash
# No cleanup needed
# Analyzing in place, no temp files
```

---

## Output Path Construction

### Base Path

```python
def construct_output_path(project_name: str) -> str:
    """Construct output directory path."""
    base = "ai_docs/documentation"
    project_folder = project_name.lower().replace(' ', '-')

    output_path = os.path.join(base, project_folder)

    # Create directory if doesn't exist
    os.makedirs(output_path, exist_ok=True)
    os.makedirs(os.path.join(output_path, "summaries"), exist_ok=True)

    return output_path

# Example:
# project_name: "MyApp"
# output_path: "ai_docs/documentation/myapp/"
```

---

## Preparation Output

### Document Created

**Location:** Output to user (not a file)

**Format:**
```markdown
## Telescope Target Prepared ✅

**Target Type:** {target_type}
**Source:** {original_input}
**Target Path:** {target_path}
**Project Name:** {project_name}
**Clone Time:** {timestamp if remote}
**Cleanup Required:** {cleanup_required}
**Ready for Analysis:** ✅

---

Next: Phase 1 - Focus Detection
```

**Example:**
```markdown
## Telescope Target Prepared ✅

**Target Type:** github
**Source:** https://github.com/anthropics/agent-starter-pack
**Target Path:** /tmp/telescope-agent-starter-pack-1696789234
**Project Name:** agent-starter-pack
**Clone Time:** 2025-10-07 14:30:00
**Cleanup Required:** true
**Ready for Analysis:** ✅

---

Next: Phase 1 - Focus Detection
```

---

## Error Messages

### Common Errors

**Path not found:**
```
❌ Error: Path does not exist: /invalid/path
💡 Tip: Verify the path is correct and accessible
```

**Clone failed:**
```
❌ Error: Failed to clone repository: https://github.com/user/repo
Reason: {error_message}

💡 Suggestions:
  - Verify the URL is correct
  - For private repos, ensure you have access and authentication
  - Check your network connection
  - Try cloning manually first: git clone {url}
  - Then analyze the local path: Telescope analyze /path/to/cloned/repo
```

**Unsupported host:**
```
❌ Error: Unsupported repository host: https://example.com/repo

💡 Supported hosts:
  - GitHub (github.com)
  - GitLab (gitlab.com)
  - Bitbucket (bitbucket.org)

💡 Alternative: Clone manually, then analyze local path
```

---

**Next Step:** Load `steps/00-preparation.md` for execution logic
