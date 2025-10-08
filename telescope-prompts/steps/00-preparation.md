# Phase 0: Target Preparation

> **Purpose:** Validate or clone the analysis target and prepare for analysis

## Prerequisites

**Must have loaded:**
- `orchestrator.md`
- `config/target-types.md`

**Input required:**
- User command with target (path or URL)
- Optional: Custom project name

## Execution Steps

### Step 1: Parse Command

```python
def parse_command(command: str) -> dict:
    """Extract target and optional custom name from command."""
    # Extract target (first argument after "analyze")
    # Could be: local path, GitHub URL, GitLab URL, Bitbucket URL

    # Extract custom name (if "as CustomName" present)
    # Example: "Telescope analyze /path as MyApp"

    return {
        "target": "extracted target",
        "custom_name": "custom name if provided, else None"
    }
```

### Step 2: Detect Target Type

```python
def detect_target_type(target: str) -> str:
    """Determine if target is local path or remote repository."""
    if "github.com" in target:
        return "github"
    elif "gitlab.com" in target:
        return "gitlab"
    elif "bitbucket.org" in target:
        return "bitbucket"
    else:
        return "local_path"
```

### Step 3: Prepare Target

**For Local Path:**

```bash
1. Validate path exists:
   if not os.path.exists(target):
     raise Error("Path does not exist: {target}")

2. Validate is directory:
   if not os.path.isdir(target):
     raise Error("Path is not a directory: {target}")

3. Validate read permissions:
   if not os.access(target, os.R_OK):
     raise Error("No read permission: {target}")

4. Set variables:
   target_path = os.path.abspath(target)
   project_name = custom_name or os.path.basename(target)
   target_type = "local_path"
   cleanup_required = False
   temp_dir = None
```

**For Remote Repository:**

```bash
1. Parse repository URL:
   repo_name = extract_repo_name(url)
   branch = extract_branch(url)  # if @branch specified

2. Create temp directory:
   timestamp = int(time.time())
   temp_dir = f"/tmp/telescope-{repo_name}-{timestamp}"

3. Clone repository:
   if branch:
     run: git clone -b {branch} {url} {temp_dir}
   else:
     run: git clone {url} {temp_dir}

4. Verify clone succeeded:
   if not os.path.exists(temp_dir):
     raise Error("Clone failed: {url}")

5. Remove .git directory (clean snapshot):
   run: rm -rf {temp_dir}/.git

6. Set variables:
   target_path = temp_dir
   project_name = custom_name or repo_name
   target_type = detected_type  # "github", "gitlab", "bitbucket"
   cleanup_required = True
   original_url = url
```

### Step 4: Format Project Name

```python
def format_project_name(name: str) -> str:
    """Format project name for directory structure."""
    return name.lower().replace(' ', '-').replace('_', '-')

project_name = format_project_name(project_name)
```

### Step 5: Construct Output Paths

```python
from pathlib import Path
from datetime import date

# Base path
base_path = Path("ai_docs") / "documentation" / project_name
summaries_path = base_path / "summaries"

# Create directories
base_path.mkdir(parents=True, exist_ok=True)
summaries_path.mkdir(exist_ok=True)

# Date string for file naming
date_str = date.today().strftime("%Y-%m-%d")
```

## Output Variables

**Phase 0 produces these variables for subsequent phases:**

```yaml
target_type: "local_path | github | gitlab | bitbucket"
target_path: "/absolute/path/to/code"
project_name: "formatted-project-name"
cleanup_required: true | false
temp_dir: "/path/to/temp" | null
original_url: "url" | null  # if remote
base_output_path: "ai_docs/documentation/{project-name}"
date_str: "YYYY-MM-DD"
```

## User Communication

**Report to user:**

```markdown
## Telescope Target Prepared ✅

**Target Type:** {target_type}
**Source:** {original input from user}
**Target Path:** {target_path}
**Project Name:** {project_name}
{**Clone Time:** {timestamp} - if remote}
{**Temp Directory:** {temp_dir} - if remote}
**Cleanup Required:** {cleanup_required}
**Output Location:** {base_output_path}
**Ready for Analysis:** ✅

---

Next: Phase 1 - Focus Detection
```

## Error Handling

### Local Path Errors

```python
try:
    validate_local_path(target)
except Exception as e:
    print(f"""
❌ Error: {e}

💡 Suggestions:
  - Verify the path is correct
  - Check that the directory exists
  - Ensure you have read permissions
  - Use absolute path if possible
""")
    exit(1)
```

### Remote Clone Errors

```python
try:
    clone_repository(url, temp_dir)
except Exception as e:
    print(f"""
❌ Error: Failed to clone repository
Reason: {e}

💡 Suggestions:
  - Verify the URL is correct
  - For private repos, ensure authentication is set up
  - Check your network connection
  - Try cloning manually first: git clone {url}
  - Then analyze the local path: Telescope analyze /path/to/cloned/repo
""")
    exit(1)
```

## Next Phase

**After successful preparation:**

1. Load `steps/01-focus-detection.md`
2. Pass variables to Phase 1
3. Continue execution

---

**Phase 0 Complete:** Target prepared and ready for analysis
