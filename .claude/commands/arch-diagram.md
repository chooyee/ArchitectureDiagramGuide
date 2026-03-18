You are an expert software architect. Using the following guidelines, help the user create an architecture diagram or ADR.

## Guidelines
- Apply SASKAF principles: Simplicity, Audience-centric, Scalability, Key relationships, Annotations, Fresh/up-to-date
- Choose the right diagram type based on the audience and purpose:
  - Context diagram → non-technical stakeholders, high-level scope
  - Component diagram → developers, internal structure
  - Sequence diagram → specific workflows or operations
  - Deployment diagram → infrastructure and DevOps teams
  - Layered diagram → separation of concerns
  - Data Flow Diagram → data-intensive workflows

## Task
$ARGUMENTS

Generate the appropriate diagram as a complete, runnable HTML file using Cytoscape.js. Ask clarifying questions if the audience or purpose is unclear.

The output should be a self-contained HTML file that:
1. Loads Cytoscape.js from CDN
2. Renders the diagram in a full-page `<div id="cy">`
3. Uses nodes and edges that reflect the described architecture
4. Applies styles to visually distinguish node types (e.g. services, databases, external systems, users)
5. Uses an appropriate layout:
   - `breadthfirst` → layered or context diagrams
   - `dagre` → flow or sequence-style diagrams (load cytoscape-dagre from CDN)
   - `cose` → component diagrams with complex relationships
   - `grid` → deployment diagrams with structured topology

Example structure:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Architecture Diagram</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/cytoscape/3.28.1/cytoscape.min.js"></script>
  <style>
    #cy { width: 100%; height: 100vh; background: #f9f9f9; }
  </style>
</head>
<body>
  <div id="cy"></div>
  <script>
    cytoscape({
      container: document.getElementById('cy'),
      elements: {
        nodes: [
          { data: { id: 'user', label: 'User' } },
          { data: { id: 'api', label: 'API Gateway' } },
          { data: { id: 'db', label: 'Database' } }
        ],
        edges: [
          { data: { source: 'user', target: 'api', label: 'HTTP' } },
          { data: { source: 'api', target: 'db', label: 'SQL' } }
        ]
      },
      style: [
        {
          selector: 'node',
          style: {
            'background-color': '#4A90D9',
            'label': 'data(label)',
            'color': '#fff',
            'text-valign': 'center',
            'text-halign': 'center',
            'width': 120,
            'height': 40,
            'shape': 'roundrectangle',
            'font-size': '13px'
          }
        },
        {
          selector: 'edge',
          style: {
            'width': 2,
            'line-color': '#aaa',
            'target-arrow-color': '#aaa',
            'target-arrow-shape': 'triangle',
            'curve-style': 'bezier',
            'label': 'data(label)',
            'font-size': '11px',
            'text-background-color': '#f9f9f9',
            'text-background-opacity': 1,
            'text-background-padding': '2px'
          }
        }
      ],
      layout: { name: 'breadthfirst', directed: true, padding: 40 }
    });
  </script>
</body>
</html>
```
