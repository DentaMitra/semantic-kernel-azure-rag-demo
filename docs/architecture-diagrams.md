# Architecture Diagrams

This repository contains comprehensive Azure architecture diagrams showcasing the semantic kernel Azure RAG demo implementation with NAT Gateway for App Service egress.

## Available Diagrams

### Global Architecture with NAT Gateway
**Source:** `diagrams/azure-architecture-nat.mmd` (Mermaid)  
**Rendered:** [SVG](images/azure-architecture-nat.svg) | [PNG](images/azure-architecture-nat.png) | [PDF](images/azure-architecture-nat.pdf)

This diagram shows the complete multi-region Azure architecture including:
- Azure Front Door for global load balancing
- Hub-spoke network topology
- **NAT Gateway for App Service outbound traffic** (key feature)
- Private endpoints for PaaS services
- Azure Firewall for AKS egress control

### Regional View with NAT Gateway Focus
**Source:** `diagrams/azure-architecture-region-nat.mmd` (Mermaid)  
**Rendered:** [SVG](images/azure-architecture-region-nat.svg) | [PNG](images/azure-architecture-region-nat.png) | [PDF](images/azure-architecture-region-nat.pdf)

A focused view of a single region highlighting:
- App Service integration subnet with NAT Gateway
- Static public IP for outbound connections
- Private Link connections to Azure PaaS services
- Network segmentation and traffic flow

### PlantUML Architecture Diagram
**Source:** `plantuml/azure-architecture-nat.puml` (PlantUML)  
**Rendered:** [SVG](images/azure-architecture-nat.svg) | [PNG](images/azure-architecture-nat.png) | [PDF](images/azure-architecture-nat.pdf)

A detailed PlantUML representation using Azure icons and standardized notation, emphasizing:
- Proper Azure service representation
- Clear data flow and dependencies
- **NAT Gateway integration for App Service egress**

### Editable Architecture Diagram
**Source:** `drawio/azure-architecture.drawio` (draw.io)  
**Rendered:** [SVG](images/azure-architecture.svg) | [PNG](images/azure-architecture.png) | [PDF](images/azure-architecture.pdf)

An editable diagram that can be opened directly in [draw.io](https://app.diagrams.net/) for:
- Interactive editing and customization
- Presentation-ready formatting
- Team collaboration on architecture changes

## Key Architecture Features

### NAT Gateway for App Service Egress
- **Static Public IP**: Provides consistent outbound IP address for App Service applications
- **Simplified Networking**: Eliminates need for complex UDR (User Defined Routes)
- **Improved Security**: Centralized egress control and monitoring
- **Better Performance**: Dedicated egress path with higher bandwidth

### Hub-Spoke Network Design
- **Centralized Services**: Shared services like Azure Firewall and Bastion in hub
- **Isolated Workloads**: Application workloads in dedicated spoke VNets
- **Controlled Connectivity**: VNet peering for secure cross-network communication

### Private Connectivity
- **Private Endpoints**: All PaaS services accessed via private connectivity
- **No Public Internet**: Backend services never exposed to public internet
- **DNS Integration**: Private DNS zones for service discovery

## Viewing Rendered Diagrams

All diagrams are automatically rendered to multiple formats on every push:

- **SVG**: Vector format, best for web viewing and documentation
- **PNG**: Raster format, good for presentations and embedding
- **PDF**: Print-ready format, ideal for documentation packages

The rendered images are available in the `docs/images/` directory and are automatically updated by the GitHub Actions workflow.

## Editing Diagrams

### Mermaid Diagrams
1. Edit `.mmd` files in the `diagrams/` directory
2. Use [Mermaid Live Editor](https://mermaid.live/) for real-time preview
3. Commit changes to trigger automatic rendering

### PlantUML Diagrams
1. Edit `.puml` files in the `plantuml/` directory
2. Use [PlantUML Online](http://www.plantuml.com/plantuml/uml/) for preview
3. Commit changes to trigger automatic rendering

### draw.io Diagrams
1. Open `drawio/azure-architecture.drawio` in [draw.io](https://app.diagrams.net/)
2. Make your changes in the visual editor
3. Save and commit the updated `.drawio` file
4. The workflow will render to image formats automatically

## Automatic Rendering Workflow

The repository includes a GitHub Actions workflow (`.github/workflows/diagram-render.yml`) that:

1. **Triggers on Changes**: Runs when diagram source files are modified
2. **Uses Kroki Service**: Leverages [kroki.io](https://kroki.io) for rendering
3. **Multiple Formats**: Generates SVG, PNG, and PDF for each diagram
4. **Auto-Commit**: Commits rendered images back to the repository
5. **Artifact Upload**: Stores rendered diagrams as build artifacts

### Kroki Integration Benefits
- **No Local Dependencies**: No need to install diagram tools locally
- **Consistent Rendering**: Same output across all environments
- **Format Support**: Supports Mermaid, PlantUML, draw.io, and many others
- **Cloud Native**: Fits well with CI/CD workflows

## Security Note

The workflow uses the public Kroki SaaS service at https://kroki.io. If your organization has policies against sending code to external services, the workflow can be modified to use local rendering tools instead:

- **Mermaid CLI**: `@mermaid-js/mermaid-cli` package
- **PlantUML**: Java-based PlantUML jar file
- **draw.io**: Headless draw.io export functionality

## Architecture Decision Records

For detailed reasoning behind architectural choices, see:
- NAT Gateway vs UDR/Azure Firewall for App Service egress
- Private endpoints vs service endpoints for PaaS connectivity
- Hub-spoke vs mesh network topology decisions