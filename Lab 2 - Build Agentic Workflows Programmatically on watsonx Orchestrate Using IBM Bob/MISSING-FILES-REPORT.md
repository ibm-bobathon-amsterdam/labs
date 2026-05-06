# Missing Files Report - Lab 2

**Date:** 2026-05-06
**Status:** ✅ RESOLVED - All Required Files Added to Repository

**Resolution Date:** 2026-05-06 12:22 UTC

---

## Summary

During the Lab 2 documentation review, I identified two critical files that are referenced in the lab instructions but are missing from the repository. These files are essential for completing STEP 1 of the lab.

---

## Missing Files

### 1. `wxo-implementation-guide.md`

**Location:** Root directory of the workspace  
**Purpose:** Comprehensive reference guide that Bob reads on demand  
**Referenced in:** `wxo-bob-lab.md` line 101  
**Impact:** HIGH - Bob cannot access detailed implementation guidelines

**Lab Instructions:**
```
1. Save `wxo-implementation-guide.md` to the root directory of your workspace.
```

**What Bob Does With This File:**
- Reads it on demand during planning and implementation
- Uses it as a comprehensive reference for watsonx Orchestrate ADK best practices
- Accesses it when the user approves (see line 145: "Bob will request access to read `wxo-implementation-guide.md`")

---

### 2. `.bob/rules/wxo-development.md`

**Location:** `.bob/rules/` directory  
**Purpose:** Concise always-on rule applied automatically across all Bob modes  
**Referenced in:** `wxo-bob-lab.md` line 103  
**Impact:** HIGH - Bob won't follow correct development patterns

**Lab Instructions:**
```
2. Create a `rules` directory inside the `.bob` folder.
3. Create `wxo-development.md` in `.bob/rules/`. Copy the required content from the GitHub repository and save it.
```

**What Bob Does With This File:**
- Automatically applies these rules across all modes (Plan, Code, Advanced, Ask)
- Ensures consistent development practices
- Follows watsonx Orchestrate ADK patterns without explicit prompting

**Visual Reference:**
- Image `images/05-bob-rule-wxo-development.png` shows what this file should look like in the Bob IDE

---

## Impact Analysis

### Without These Files:

1. **STEP 1 Cannot Be Completed**
   - Users cannot proceed with the lab as instructed
   - The lab explicitly requires these files before moving to STEP 2

2. **Bob Lacks Critical Context**
   - Bob won't have watsonx Orchestrate ADK best practices
   - Generated code may not follow correct patterns
   - Implementation may deviate from IBM standards

3. **User Experience Issues**
   - Confusion about where to find these files
   - Lab instructions say "Copy the required content from the GitHub repository" but don't specify which repository
   - No fallback or alternative instructions provided

---

## Current Lab References

### File Purpose Table (from wxo-bob-lab.md lines 94-97)

| File | Purpose |
|------|---------|
| `wxo-implementation-guide.md` (root) | Comprehensive reference guide Bob reads on demand |
| `.bob/rules/wxo-development.md` | Concise always-on rule applied automatically across all modes |

### STEP 1 Instructions (lines 100-105)

```markdown
**Steps:**

1. Save `wxo-implementation-guide.md` to the root directory of your workspace.
2. Create a `rules` directory inside the `.bob` folder.
3. Create `wxo-development.md` in `.bob/rules/`. Copy the required content from the GitHub repository and save it.

![wxo-development.md rule file in Bob IDE](images/05-bob-rule-wxo-development.png)
```

### STEP 2 Reference (line 145)

```markdown
3. Bob will request access to read `wxo-implementation-guide.md`. Click **Approve**.
```

---

## Source Information

**Tutorial Source:**  
[IBM Developer - Build agentic workflows with watsonx Orchestrate and IBM Bob](https://developer.ibm.com/tutorials/build-programmatic-agentic-workflows-watsonx-orchestrate-bob/)

**Authors:**  
- Allen Chan
- Ahmed Azraq  
- Syeda Ameena Begum

**Published:** 09 February 2026

---

## Recommended Actions

### Immediate (Required)

1. ✅ **Obtain Original Files from IBM**
   - Contact tutorial authors or IBM Developer team
   - Request the original `wxo-implementation-guide.md` and `wxo-development.md` files
   - Verify files are the official versions used in the published tutorial

2. **Add Files to Repository**
   - Place `wxo-implementation-guide.md` in the Lab 2 root directory
   - Create `.bob/rules/` directory structure
   - Place `wxo-development.md` in `.bob/rules/`

3. **Verify File Placement**
   - Ensure files match the lab instructions exactly
   - Test that Bob can access both files as described
   - Confirm image `05-bob-rule-wxo-development.png` matches the actual file content

### Documentation Updates (If Needed)

1. **If Files Are Instructor-Provided:**
   - Update STEP 1 to clarify files will be provided by instructor
   - Add download links or distribution method
   - Include file checksums for verification

2. **If Files Are Public:**
   - Add direct download links to the lab instructions
   - Update "Copy the required content from the GitHub repository" to specify exact repository URL
   - Consider including files directly in this repository

3. **Add Prerequisites Note:**
   - Update Lab 2 README.md to mention these required files
   - Add to the prerequisites checklist
   - Include in the "Before You Begin" section

---

## File Structure After Resolution

```
Lab 2 - Build Agentic Workflows.../
├── wxo-implementation-guide.md          ← ADD THIS FILE
├── .bob/
│   ├── rules/
│   │   └── wxo-development.md           ← ADD THIS FILE
│   └── mcp.json
├── wxo-bob-lab.md
├── README.md
├── Prerequisites/
└── images/
```

---

## Additional Files to Review

While investigating, I should also check if there are any other files referenced in the lab that might be missing:

- ✅ `env setup instructions.pdf` - EXISTS
- ✅ All image files (01-29) - EXIST
- ❓ Any sample invoice PDFs for testing - NOT CHECKED
- ❓ Any example code snippets - NOT CHECKED

---

## Status Updates

**2026-05-06 12:15 UTC:**
- ✅ Identified missing files
- ✅ Documented impact and requirements
- ✅ Created this report
- ⏳ Waiting for original files from IBM

**2026-05-06 12:22 UTC - RESOLVED:**
- ✅ Located files in IBM GitHub repository: https://github.com/IBM/oic-i-agentic-ai-tutorials/tree/main/bob-wxo-dev
- ✅ Downloaded `wxo-implementation-guide.md` (38KB)
- ✅ Downloaded `.bob/rules/wxo-development.md` (1.2KB)
- ✅ Downloaded `sample-pdfs/flight.pdf` (297KB)
- ✅ Updated lab documentation with GitHub source reference
- ✅ All files verified in correct locations

**Files Now Available:**
```
Lab 2.../
├── wxo-implementation-guide.md          ✅ Added
├── .bob/
│   └── rules/
│       └── wxo-development.md           ✅ Added
└── sample-pdfs/
    └── flight.pdf                       ✅ Added
```

**Lab Status:** Ready for use - all required files are now in the repository

---

## Contact

For questions about this report or to provide the missing files, please contact the repository maintainer.

**Related Issues:**
- Missing files prevent lab completion
- Lab instructions reference non-existent GitHub repository
- No fallback instructions provided