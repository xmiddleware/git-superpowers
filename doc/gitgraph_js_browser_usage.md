# GitGraph.js - Complete Browser Usage Guide

## Table of Contents
1. [Overview](#overview)
2. [Installation Methods](#installation-methods)
3. [Basic Setup](#basic-setup)
4. [Basic Usage](#basic-usage)
5. [Configuration Options](#configuration-options)
6. [Advanced Features](#advanced-features)
7. [Common Patterns](#common-patterns)
8. [Styling & Customization](#styling--customization)
9. [Event Handling](#event-handling)
10. [Troubleshooting](#troubleshooting)
11. [Best Practices](#best-practices)
12. [Complete Examples](#complete-examples)

---

## Overview

**GitGraph.js** is a JavaScript library that allows you to draw beautiful, interactive Git graphs directly in your browser. It provides a programmatic API to visualize Git workflows, branch structures, commits, merges, and tags.

### Key Features
- 🎨 Beautiful, customizable Git graph visualizations
- 📱 Responsive and interactive
- 🔧 Highly configurable (orientation, templates, colors)
- 🎯 Event handling (click, hover, etc.)
- 📦 Works directly in the browser (no build step required)
- 🚀 Lightweight and performant

### Important Note
⚠️ **The GitGraph.js project was archived in July 2024** and is no longer actively maintained. However, it remains functional and can still be used for projects. For new projects, you may want to consider alternatives like Mermaid.js.

---

## Installation Methods

### Method 1: CDN (Recommended for Quick Start)

The easiest way to use GitGraph.js in the browser is via a CDN. Add these script tags to your HTML:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GitGraph Example</title>
</head>
<body>
    <!-- Container for the graph -->
    <div id="gitgraph"></div>

    <!-- GitGraph.js from CDN -->
    <script src="https://cdn.jsdelivr.net/npm/@gitgraph/js@1.4.0/dist/gitgraph.umd.min.js"></script>
    
    <script>
        // Your GitGraph code here
    </script>
</body>
</html>
```

### Method 2: Download and Host Locally

1. **Download the library:**
   - Visit: https://github.com/nicoespeon/gitgraph.js/releases
   - Download the latest `gitgraph.umd.min.js` file
   - Or use: `https://unpkg.com/@gitgraph/js@1.4.0/dist/gitgraph.umd.min.js`

2. **Include in your HTML:**
```html
<script src="./js/gitgraph.umd.min.js"></script>
```

### Method 3: NPM (For Build Tools)

If you're using a build tool (Webpack, Vite, etc.):

```bash
npm install @gitgraph/js
```

Then import in your JavaScript:
```javascript
import { createGitgraph } from "@gitgraph/js";
```

---

## Basic Setup

### Step 1: Create HTML Container

Create a container element where the graph will be rendered:

```html
<div id="gitgraph-container"></div>
```

**Important:** The container should have a defined width and height:

```html
<div id="gitgraph-container" style="width: 100%; height: 500px;"></div>
```

Or use CSS:
```css
#gitgraph-container {
    width: 100%;
    height: 500px;
    border: 1px solid #ddd;
    border-radius: 4px;
    padding: 20px;
}
```

### Step 2: Initialize GitGraph

```javascript
// Get the container element
const graphContainer = document.getElementById("gitgraph-container");

// Create GitGraph instance
const gitgraph = GitgraphJS.createGitgraph(graphContainer);
```

**Note:** If using CDN, the library is available as `GitgraphJS` in the global scope. If using ES modules, use `createGitgraph` directly.

---

## Basic Usage

### Creating Branches and Commits

```javascript
// Create the main branch (usually 'master' or 'main')
const master = gitgraph.branch("master");

// Make commits on the master branch
master.commit("Initial commit");
master.commit("Add README");
master.commit("Add configuration files");
```

### Creating Feature Branches

```javascript
// Create a feature branch from master
const feature = gitgraph.branch("feature/user-authentication");

// Make commits on the feature branch
feature.commit("Add login form");
feature.commit("Implement authentication logic");
feature.commit("Add tests");

// Merge feature branch back to master
master.merge(feature, "Merge feature: user authentication");
```

### Adding Tags

```javascript
// Add a tag to mark a release
master.tag("v1.0.0");
```

### Complete Basic Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GitGraph Basic Example</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 20px;
        }
        #gitgraph {
            width: 100%;
            height: 600px;
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 20px;
            background: #fff;
        }
    </style>
</head>
<body>
    <h1>Git Graph Visualization</h1>
    <div id="gitgraph"></div>

    <script src="https://cdn.jsdelivr.net/npm/@gitgraph/js@1.4.0/dist/gitgraph.umd.min.js"></script>
    <script>
        const graphContainer = document.getElementById("gitgraph");
        const gitgraph = GitgraphJS.createGitgraph(graphContainer);

        // Create main branch
        const master = gitgraph.branch("master");
        master.commit("Initial commit");
        master.commit("Add README");
        master.commit("Add configuration");

        // Create feature branch
        const feature = gitgraph.branch("feature/new-feature");
        feature.commit("Start new feature");
        feature.commit("Implement core functionality");
        feature.commit("Add tests");

        // Continue on master
        master.commit("Fix bug in production");

        // Merge feature
        master.merge(feature, "Merge new feature");

        // Tag release
        master.tag("v1.0.0");
    </script>
</body>
</html>
```

---

## Configuration Options

### Graph Orientation

Control the direction of the graph:

```javascript
const gitgraph = GitgraphJS.createGitgraph(graphContainer, {
    orientation: "vertical" // Options: "vertical", "vertical-reverse", "horizontal", "horizontal-reverse"
});
```

**Options:**
- `"vertical"` - Top to bottom (default)
- `"vertical-reverse"` - Bottom to top
- `"horizontal"` - Left to right
- `"horizontal-reverse"` - Right to left

### Template Selection

Choose a visual template:

```javascript
const gitgraph = GitgraphJS.createGitgraph(graphContainer, {
    template: "metro" // Options: "metro", "blackarrow", or custom template
});
```

**Templates:**
- `"metro"` - Modern, colorful design (default)
- `"blackarrow"` - Classic black and white with arrows

### Display Mode

Control how commits are displayed:

```javascript
const gitgraph = GitgraphJS.createGitgraph(graphContainer, {
    mode: "compact" // Options: "normal" (default), "compact"
});
```

**Modes:**
- `"normal"` - Shows commit messages inline
- `"compact"` - Hides commit messages, shows them in tooltips on hover

### Complete Configuration Example

```javascript
const gitgraph = GitgraphJS.createGitgraph(graphContainer, {
    orientation: "vertical",
    template: "metro",
    mode: "normal",
    author: "John Doe <john@example.com>",
    commitMessage: "Default commit message",
    branchLabelOnEveryCommit: false,
    theme: {
        colors: ["#008fb5", "#979797", "#df0052", "#faded3"],
        branch: {
            lineWidth: 3,
            spacing: 50,
            mergeStyle: "bezier",
            labelRotation: 0
        },
        commit: {
            spacing: 50,
            dot: {
                size: 8,
                strokeWidth: 2
            },
            message: {
                display: true,
                displayAuthor: false,
                displayHash: true,
                font: "normal 12pt Arial"
            }
        }
    }
});
```

---

## Advanced Features

### Custom Branch Styling

```javascript
const feature = gitgraph.branch({
    name: "feature/custom-styled",
    style: {
        lineWidth: 4,
        spacing: 60,
        stroke: "#ff6b6b",
        label: {
            bgColor: "#ff6b6b",
            color: "#fff",
            strokeColor: "#c92a2a",
            borderRadius: 5,
            font: "bold 12pt Arial"
        }
    }
});
```

### Custom Commit Options

```javascript
master.commit({
    subject: "Add new feature",
    body: "This commit adds a comprehensive new feature with multiple components.",
    author: "Jane Doe <jane@example.com>",
    hash: "abc123",
    dotText: "⭐",
    style: {
        message: {
            color: "#333",
            font: "bold 12pt Arial"
        },
        dot: {
            size: 10,
            strokeWidth: 3,
            fill: "#4ecdc4"
        }
    }
});
```

### Commit with Custom Dot Text

```javascript
master.commit({
    subject: "Release v1.0",
    dotText: "🚀"
});
```

### Merge Options

```javascript
master.merge({
    branch: feature,
    commitOptions: {
        subject: "Merge feature branch",
        body: "Merged feature/custom-styled into master",
        style: {
            message: {
                color: "#0066cc"
            }
        }
    },
    fastForward: false // Set to true for fast-forward merges
});
```

### Multiple Branches and Complex Workflows

```javascript
const gitgraph = GitgraphJS.createGitgraph(graphContainer);

// Main branch
const main = gitgraph.branch("main");
main.commit("Initial commit");
main.commit("Setup project structure");

// Development branch
const develop = gitgraph.branch("develop");
develop.commit("Add development config");
develop.commit("Setup CI/CD");

// Feature branches
const feature1 = develop.branch("feature/user-login");
feature1.commit("Create login form");
feature1.commit("Add authentication logic");

const feature2 = develop.branch("feature/dashboard");
feature2.commit("Create dashboard layout");
feature2.commit("Add widgets");

// Merge features
develop.merge(feature1, "Merge user login feature");
develop.merge(feature2, "Merge dashboard feature");

// Hotfix on main
const hotfix = main.branch("hotfix/security-patch");
hotfix.commit("Fix security vulnerability");
main.merge(hotfix, "Merge security hotfix");
main.tag("v1.0.1");

// Merge develop to main
main.merge(develop, "Release v1.1.0");
main.tag("v1.1.0");
```

---

## Common Patterns

### Git Flow Workflow

```javascript
const gitgraph = GitgraphJS.createGitgraph(graphContainer);

// Main branches
const master = gitgraph.branch("master");
master.commit("Initial commit");

const develop = gitgraph.branch("develop");
develop.commit("Setup development environment");

// Feature branch
const feature = develop.branch("feature/new-feature");
feature.commit("Start feature");
feature.commit("Implement feature");
develop.merge(feature, "Merge feature");

// Release branch
const release = develop.branch("release/v1.0");
release.commit("Prepare release");
release.commit("Fix bugs");
master.merge(release, "Release v1.0");
master.tag("v1.0.0");
develop.merge(release, "Merge release back to develop");

// Hotfix branch
const hotfix = master.branch("hotfix/critical-bug");
hotfix.commit("Fix critical bug");
master.merge(hotfix, "Hotfix v1.0.1");
master.tag("v1.0.1");
develop.merge(hotfix, "Merge hotfix to develop");
```

### GitHub Flow (Simple Workflow)

```javascript
const gitgraph = GitgraphJS.createGitgraph(graphContainer);

const main = gitgraph.branch("main");
main.commit("Initial commit");
main.commit("Add basic features");

// Feature branches
const feature1 = main.branch("feature/add-login");
feature1.commit("Add login page");
feature1.commit("Add authentication");
main.merge(feature1, "Merge PR #1");

const feature2 = main.branch("feature/add-dashboard");
feature2.commit("Create dashboard");
main.merge(feature2, "Merge PR #2");

main.tag("v1.0.0");
```

### Rebase Workflow

```javascript
const gitgraph = GitgraphJS.createGitgraph(graphContainer);

const master = gitgraph.branch("master");
master.commit("Commit A");
master.commit("Commit B");

const feature = gitgraph.branch("feature");
feature.commit("Commit C");
feature.commit("Commit D");

// Simulate rebase (create new commits on top of updated master)
master.commit("Commit E");
const featureRebased = master.branch("feature-rebased");
featureRebased.commit("Commit C' (rebased)");
featureRebased.commit("Commit D' (rebased)");
master.merge(featureRebased, "Merge rebased feature");
```

---

## Styling & Customization

### Custom Theme

```javascript
const gitgraph = GitgraphJS.createGitgraph(graphContainer, {
    theme: {
        colors: ["#008fb5", "#979797", "#df0052", "#faded3", "#c9d6d8"],
        branch: {
            lineWidth: 4,
            spacing: 50,
            mergeStyle: "bezier", // or "straight"
            labelRotation: 0,
            labelBgColor: "#fff",
            labelColor: "#000"
        },
        commit: {
            spacing: 50,
            dot: {
                size: 10,
                strokeWidth: 3,
                strokeColor: "#000"
            },
            message: {
                display: true,
                displayAuthor: true,
                displayHash: true,
                font: "normal 12pt Arial",
                color: "#333"
            }
        },
        tag: {
            font: "bold 10pt Arial",
            color: "#333",
            bgColor: "#ffd700",
            borderColor: "#ffa500",
            borderRadius: 3,
            pointerWidth: 6
        }
    }
});
```

### Per-Branch Styling

```javascript
const feature = gitgraph.branch({
    name: "feature/custom",
    style: {
        lineWidth: 5,
        spacing: 60,
        stroke: "#ff6b6b",
        label: {
            bgColor: "#ff6b6b",
            color: "#fff",
            strokeColor: "#c92a2a",
            borderRadius: 5,
            font: "bold 14pt Arial"
        }
    }
});
```

### Per-Commit Styling

```javascript
master.commit({
    subject: "Styled commit",
    style: {
        dot: {
            size: 12,
            strokeWidth: 4,
            fill: "#4ecdc4",
            strokeColor: "#2d9cdb"
        },
        message: {
            color: "#2d9cdb",
            font: "bold 13pt Arial"
        }
    }
});
```

---

## Event Handling

### Click Events

```javascript
master.commit({
    subject: "Clickable commit",
    onClick: (commit) => {
        console.log("Commit clicked:", commit);
        alert(`Commit: ${commit.subject}\nHash: ${commit.hash}`);
    }
});
```

### Hover Events

```javascript
master.commit({
    subject: "Interactive commit",
    onMouseOver: (commit) => {
        console.log("Mouse over commit:", commit);
        // Add custom hover effects
    },
    onMouseOut: (commit) => {
        console.log("Mouse out of commit:", commit);
        // Remove hover effects
    }
});
```

### Complete Event Example

```javascript
const gitgraph = GitgraphJS.createGitgraph(graphContainer);

const master = gitgraph.branch("master");

master.commit({
    subject: "Initial commit",
    onClick: (commit) => {
        document.getElementById("commit-info").innerHTML = `
            <h3>Commit Details</h3>
            <p><strong>Subject:</strong> ${commit.subject}</p>
            <p><strong>Hash:</strong> ${commit.hash}</p>
            <p><strong>Author:</strong> ${commit.author}</p>
        `;
    },
    onMouseOver: (commit) => {
        console.log("Hovering over:", commit.subject);
    }
});

// HTML element to display commit info
// <div id="commit-info"></div>
```

---

## Troubleshooting

### Graph Not Displaying

**Problem:** The graph doesn't appear on the page.

**Solutions:**
1. **Check container dimensions:**
   ```css
   #gitgraph-container {
       width: 100%;
       height: 500px; /* Must have explicit height */
   }
   ```

2. **Verify script is loaded:**
   ```javascript
   console.log(typeof GitgraphJS); // Should output "object"
   ```

3. **Check browser console for errors**

4. **Ensure container exists before initialization:**
   ```javascript
   document.addEventListener("DOMContentLoaded", () => {
       const container = document.getElementById("gitgraph");
       const gitgraph = GitgraphJS.createGitgraph(container);
       // ... rest of code
   });
   ```

### Commits Not Showing

**Problem:** Commits are created but not visible.

**Solutions:**
1. Ensure you're calling `.commit()` on a branch object
2. Check that the branch was created correctly
3. Verify the container has proper dimensions

### Styling Not Applied

**Problem:** Custom styles aren't being applied.

**Solutions:**
1. Check the theme structure matches the expected format
2. Verify color values are valid (hex, rgb, etc.)
3. Ensure style options are passed correctly

### CDN Not Loading

**Problem:** CDN script fails to load.

**Solutions:**
1. Check internet connection
2. Try a different CDN:
   ```html
   <script src="https://unpkg.com/@gitgraph/js@1.4.0/dist/gitgraph.umd.min.js"></script>
   ```
3. Download and host locally

---

## Best Practices

### 1. Always Set Container Dimensions

```html
<div id="gitgraph" style="width: 100%; height: 600px;"></div>
```

### 2. Initialize After DOM Load

```javascript
document.addEventListener("DOMContentLoaded", () => {
    // Initialize GitGraph here
});
```

### 3. Use Meaningful Commit Messages

```javascript
// Good
master.commit("Add user authentication with JWT tokens");

// Bad
master.commit("fix");
```

### 4. Organize Complex Workflows

For complex graphs, break them into logical sections:

```javascript
// Setup
const gitgraph = GitgraphJS.createGitgraph(container);
const main = gitgraph.branch("main");
main.commit("Initial commit");

// Feature development
function createFeature(name) {
    const feature = main.branch(`feature/${name}`);
    feature.commit(`Start ${name}`);
    feature.commit(`Implement ${name}`);
    return feature;
}

const loginFeature = createFeature("login");
const dashboardFeature = createFeature("dashboard");

// Merging
main.merge(loginFeature, "Merge login feature");
main.merge(dashboardFeature, "Merge dashboard feature");
```

### 5. Use Configuration Objects

Instead of passing many individual options, use configuration objects:

```javascript
const config = {
    orientation: "vertical",
    template: "metro",
    mode: "normal"
};
const gitgraph = GitgraphJS.createGitgraph(container, config);
```

### 6. Handle Errors Gracefully

```javascript
try {
    const gitgraph = GitgraphJS.createGitgraph(container);
    // ... your code
} catch (error) {
    console.error("Error creating GitGraph:", error);
    container.innerHTML = "<p>Error loading graph. Please refresh the page.</p>";
}
```

---

## Complete Examples

### Example 1: Simple Project History

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Git History</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        #gitgraph {
            width: 100%;
            height: 500px;
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 20px;
            background: #fff;
            margin: 20px 0;
        }
    </style>
</head>
<body>
    <h1>Project Git History</h1>
    <div id="gitgraph"></div>

    <script src="https://cdn.jsdelivr.net/npm/@gitgraph/js@1.4.0/dist/gitgraph.umd.min.js"></script>
    <script>
        document.addEventListener("DOMContentLoaded", () => {
            const container = document.getElementById("gitgraph");
            const gitgraph = GitgraphJS.createGitgraph(container, {
                orientation: "vertical",
                template: "metro"
            });

            const master = gitgraph.branch("master");
            master.commit("Project initialization");
            master.commit("Add project structure");
            master.commit("Setup build configuration");

            const develop = gitgraph.branch("develop");
            develop.commit("Setup development environment");

            const feature = develop.branch("feature/user-management");
            feature.commit("Create user model");
            feature.commit("Add user authentication");
            feature.commit("Implement user CRUD operations");

            develop.merge(feature, "Merge user management feature");
            master.merge(develop, "Release v1.0.0");
            master.tag("v1.0.0");
        });
    </script>
</body>
</html>
```

### Example 2: Interactive Git Graph

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Git Graph</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }
        .container {
            display: flex;
            gap: 20px;
        }
        #gitgraph {
            flex: 2;
            height: 700px;
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 20px;
            background: #fff;
        }
        #commit-info {
            flex: 1;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 8px;
            background: #f9f9f9;
        }
        #commit-info h3 {
            margin-top: 0;
        }
        .commit-detail {
            margin: 10px 0;
            padding: 10px;
            background: #fff;
            border-radius: 4px;
        }
    </style>
</head>
<body>
    <h1>Interactive Git Graph</h1>
    <div class="container">
        <div id="gitgraph"></div>
        <div id="commit-info">
            <h3>Commit Information</h3>
            <p>Click on a commit to see details</p>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/@gitgraph/js@1.4.0/dist/gitgraph.umd.min.js"></script>
    <script>
        document.addEventListener("DOMContentLoaded", () => {
            const container = document.getElementById("gitgraph");
            const infoPanel = document.getElementById("commit-info");
            
            const gitgraph = GitgraphJS.createGitgraph(container, {
                orientation: "vertical",
                template: "metro",
                mode: "normal"
            });

            function displayCommitInfo(commit) {
                infoPanel.innerHTML = `
                    <h3>Commit Details</h3>
                    <div class="commit-detail">
                        <strong>Subject:</strong> ${commit.subject || "N/A"}
                    </div>
                    <div class="commit-detail">
                        <strong>Hash:</strong> ${commit.hash || "N/A"}
                    </div>
                    <div class="commit-detail">
                        <strong>Author:</strong> ${commit.author || "N/A"}
                    </div>
                    <div class="commit-detail">
                        <strong>Body:</strong> ${commit.body || "No body"}
                    </div>
                `;
            }

            const master = gitgraph.branch("master");
            master.commit({
                subject: "Initial commit",
                onClick: displayCommitInfo
            });
            master.commit({
                subject: "Add README",
                body: "Added comprehensive README with setup instructions",
                onClick: displayCommitInfo
            });
            master.commit({
                subject: "Setup project structure",
                onClick: displayCommitInfo
            });

            const feature = gitgraph.branch("feature/new-feature");
            feature.commit({
                subject: "Start new feature",
                onClick: displayCommitInfo
            });
            feature.commit({
                subject: "Implement core functionality",
                body: "Implemented the main feature logic with tests",
                onClick: displayCommitInfo
            });
            feature.commit({
                subject: "Add documentation",
                onClick: displayCommitInfo
            });

            master.commit({
                subject: "Fix bug in production",
                onClick: displayCommitInfo
            });

            master.merge(feature, {
                subject: "Merge new feature",
                onClick: displayCommitInfo
            });

            master.tag("v1.0.0");
        });
    </script>
</body>
</html>
```

### Example 3: Custom Styled Git Flow

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Custom Styled Git Flow</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            background: #f5f5f5;
        }
        #gitgraph {
            width: 100%;
            height: 800px;
            border: 2px solid #333;
            border-radius: 12px;
            padding: 30px;
            background: #fff;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
    </style>
</head>
<body>
    <h1>Git Flow Workflow Visualization</h1>
    <div id="gitgraph"></div>

    <script src="https://cdn.jsdelivr.net/npm/@gitgraph/js@1.4.0/dist/gitgraph.umd.min.js"></script>
    <script>
        document.addEventListener("DOMContentLoaded", () => {
            const container = document.getElementById("gitgraph");
            const gitgraph = GitgraphJS.createGitgraph(container, {
                orientation: "vertical",
                template: "metro",
                theme: {
                    colors: ["#008fb5", "#979797", "#df0052", "#faded3", "#c9d6d8"],
                    branch: {
                        lineWidth: 4,
                        spacing: 60,
                        labelRotation: 0
                    },
                    commit: {
                        spacing: 60,
                        dot: {
                            size: 10,
                            strokeWidth: 3
                        },
                        message: {
                            display: true,
                            displayAuthor: false,
                            displayHash: true,
                            font: "normal 12pt 'Segoe UI'"
                        }
                    }
                }
            });

            // Master branch
            const master = gitgraph.branch({
                name: "master",
                style: {
                    stroke: "#008fb5",
                    label: {
                        bgColor: "#008fb5",
                        color: "#fff"
                    }
                }
            });
            master.commit("Initial commit");
            master.commit("Setup project");

            // Develop branch
            const develop = gitgraph.branch({
                name: "develop",
                style: {
                    stroke: "#979797",
                    label: {
                        bgColor: "#979797",
                        color: "#fff"
                    }
                }
            });
            develop.commit("Setup development environment");

            // Feature branches
            const feature1 = develop.branch({
                name: "feature/login",
                style: {
                    stroke: "#df0052",
                    label: {
                        bgColor: "#df0052",
                        color: "#fff"
                    }
                }
            });
            feature1.commit("Create login form");
            feature1.commit("Add authentication");

            const feature2 = develop.branch({
                name: "feature/dashboard",
                style: {
                    stroke: "#faded3",
                    label: {
                        bgColor: "#faded3",
                        color: "#333"
                    }
                }
            });
            feature2.commit("Create dashboard");
            feature2.commit("Add widgets");

            // Merge features
            develop.merge(feature1, "Merge login feature");
            develop.merge(feature2, "Merge dashboard feature");

            // Release branch
            const release = develop.branch({
                name: "release/v1.0",
                style: {
                    stroke: "#c9d6d8",
                    label: {
                        bgColor: "#c9d6d8",
                        color: "#333"
                    }
                }
            });
            release.commit("Prepare release");
            release.commit("Fix bugs");

            master.merge(release, "Release v1.0.0");
            master.tag("v1.0.0");
            develop.merge(release, "Merge release back");

            // Hotfix
            const hotfix = master.branch({
                name: "hotfix/critical",
                style: {
                    stroke: "#ff6b6b",
                    label: {
                        bgColor: "#ff6b6b",
                        color: "#fff"
                    }
                }
            });
            hotfix.commit("Fix critical bug");
            master.merge(hotfix, "Hotfix v1.0.1");
            master.tag("v1.0.1");
            develop.merge(hotfix, "Merge hotfix to develop");
        });
    </script>
</body>
</html>
```

---

## Additional Resources

- **GitHub Repository:** https://github.com/nicoespeon/gitgraph.js
- **NPM Package:** https://www.npmjs.com/package/@gitgraph/js
- **Documentation:** Check the repository's README and examples
- **Alternative:** Consider [Mermaid.js](https://mermaid.js.org/) for newer projects

---

## Summary

GitGraph.js is a powerful library for visualizing Git workflows in the browser. Key takeaways:

1. ✅ Easy to set up with CDN or npm
2. ✅ Highly customizable with themes and styles
3. ✅ Supports complex workflows (Git Flow, GitHub Flow, etc.)
4. ✅ Interactive with event handling
5. ✅ Works directly in the browser without build tools

Remember: The project is archived but still functional. For new projects, consider evaluating alternatives like Mermaid.js.

---

**Happy Git Graphing! 🚀**

