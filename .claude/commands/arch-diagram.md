You are an expert software architect. Your job is to analyze a code repository, understand its architecture, and produce two output files.

## Step 1: Explore the Repository

Thoroughly explore the codebase provided in $ARGUMENTS (or the current working directory if no path is given):
- Identify all major components, services, modules, and layers
- Understand how they communicate (APIs, events, queues, direct calls, imports)
- Identify external dependencies, databases, and third-party services
- Note the technology stack for each component

## Step 2: Generate the Cytoscape.js Diagram

Write a self-contained `architecture-diagram.html` file using Cytoscape.js that visualizes the architecture.

Rules:
- Use distinct node shapes/colors to differentiate component types:
  - Services / modules → roundrectangle, blue (#4A90D9)
  - Databases / storage → ellipse, green (#27AE60)
  - External systems / third-party → rectangle, orange (#E67E22)
  - Users / clients → ellipse, grey (#7F8C8D)
  - Message queues / events → diamond, purple (#8E44AD)
- Label edges with the communication method (e.g. REST, gRPC, SQL, event, import)
- Choose layout based on architecture style:
  - `breadthfirst` → layered or monolithic
  - `cose` → microservices or complex component graphs
  - `dagre` → flow or pipeline architectures (load cytoscape-dagre from CDN)
  - `grid` → deployment / infrastructure diagrams

The HTML file structure:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Architecture Diagram</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/cytoscape/3.28.1/cytoscape.min.js"></script>
  <style>
    body { margin: 0; }
    #cy { width: 100%; height: 100vh; background: #f9f9f9; }
  </style>
</head>
<body>
  <div id="cy"></div>
  <script>
    cytoscape({
      container: document.getElementById('cy'),
      elements: {
        nodes: [ /* derived from repo analysis */ ],
        edges: [ /* derived from repo analysis */ ]
      },
      style: [ /* node and edge styles */ ],
      layout: { name: 'cose', padding: 40 }
    });
  </script>
</body>
</html>
```

## Step 3: Generate the Architecture Markdown

Write an `architecture.md` file covering:

```markdown
# Architecture Overview

## Tech Stack
- List languages, frameworks, and runtimes

## Components
For each component: name, responsibility, technology

## Component Interactions
How components communicate and depend on each other

## Data Flow
How data moves through the system for key operations

## External Dependencies
Third-party services, APIs, databases

## Architectural Style
Identify the pattern (microservices, monolith, layered, event-driven, etc.) and justify based on findings

## Key Observations
Notable design decisions, potential risks, or areas of interest
```

## Output

Write both files to the same directory as the analyzed repository:
1. `architecture-diagram.html` — interactive Cytoscape.js diagram
2. `architecture.md` — architecture documentation in markdown
