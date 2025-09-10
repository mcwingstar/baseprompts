# AI Agent Instructions: Create a Great GitLab Repository for Markdown

## Overview
You are an AI assistant helping to create and optimize a GitLab repository specifically designed for markdown content. Your goal is to set up a professional, well-organized repository that follows best practices for documentation, collaboration, and maintenance.

## Core Objectives
1. **Structure**: Create a logical, scalable folder structure for markdown files
2. **Documentation**: Implement comprehensive documentation standards
3. **Automation**: Set up CI/CD pipelines for markdown validation and processing
4. **Collaboration**: Configure tools and templates for team collaboration
5. **Quality**: Ensure consistent formatting and style across all markdown files

## Repository Structure to Implement

### 1. Root Directory Setup
```
├── .gitlab/
│   ├── ci/
│   │   └── markdown-validation.yml
│   └── issue_templates/
│       ├── documentation-bug.md
│       └── content-request.md
├── docs/
│   ├── getting-started/
│   ├── guides/
│   ├── api/
│   └── examples/
├── templates/
│   ├── article-template.md
│   ├── guide-template.md
│   └── api-doc-template.md
├── assets/
│   ├── images/
│   └── diagrams/
├── .markdownlint.json
├── .gitignore
├── README.md
├── CONTRIBUTING.md
└── LICENSE
```

### 2. Essential Files to Create

#### README.md
- Project overview and purpose
- Quick start guide
- Table of contents with links
- Badges for build status, license, etc.
- Contributing guidelines reference
- Contact information

#### CONTRIBUTING.md
- How to contribute guidelines
- Markdown style guide
- Pull request process
- Issue reporting guidelines
- Code of conduct

#### .markdownlint.json
- Configure markdown linting rules
- Set line length limits
- Define heading styles
- Configure list formatting

#### .gitignore
- Ignore temporary files
- Exclude build artifacts
- Ignore IDE-specific files
- Exclude generated documentation

### 3. GitLab CI/CD Pipeline

#### markdown-validation.yml
```yaml
stages:
  - validate
  - build
  - deploy

markdown_lint:
  stage: validate
  image: node:latest
  script:
    - npm install -g markdownlint-cli
    - markdownlint "**/*.md" --ignore node_modules
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH

build_docs:
  stage: build
  image: node:latest
  script:
    - npm install -g docsify-cli
    - docsify serve docs --port 3000
  artifacts:
    paths:
      - docs/_site/
    expire_in: 1 week
```

### 4. Documentation Standards

#### Markdown Style Guide
- Use consistent heading hierarchy (H1 for page titles, H2 for sections)
- Limit line length to 80-100 characters
- Use descriptive link text
- Include alt text for images
- Use code blocks with language specification
- Follow consistent list formatting

#### File Naming Conventions
- Use kebab-case for file names
- Include descriptive names
- Use numbers for ordering when needed (01-introduction.md)
- Avoid special characters and spaces

#### Content Organization
- Group related content in folders
- Use index files for navigation
- Include cross-references between documents
- Maintain a logical flow from basic to advanced topics

### 5. Collaboration Features

#### Issue Templates
- Documentation bug report template
- Content request template
- Feature request template
- Template for new contributor onboarding

#### Merge Request Templates
- Checklist for markdown quality
- Review guidelines
- Testing requirements
- Documentation update requirements

#### Branch Protection Rules
- Require merge request reviews
- Require status checks to pass
- Restrict pushes to main branch
- Require up-to-date branches

### 6. Quality Assurance

#### Automated Checks
- Markdown syntax validation
- Link checking
- Image optimization
- Spelling and grammar checks
- Accessibility compliance

#### Manual Review Process
- Content accuracy review
- Style consistency check
- User experience evaluation
- Technical accuracy verification

### 7. Advanced Features

#### Search and Navigation
- Implement full-text search
- Create navigation menus
- Add breadcrumb navigation
- Include table of contents

#### Version Control
- Tag releases for documentation versions
- Maintain changelog
- Archive old versions
- Track documentation metrics

#### Integration
- Connect with project management tools
- Integrate with communication platforms
- Set up automated notifications
- Configure webhooks for updates

## Implementation Steps

1. **Initialize Repository Structure**
   - Create folder hierarchy
   - Set up initial configuration files
   - Configure GitLab project settings

2. **Set Up CI/CD Pipeline**
   - Create validation pipeline
   - Configure build and deployment
   - Test pipeline functionality

3. **Create Documentation Templates**
   - Design consistent templates
   - Create style guide
   - Set up contribution guidelines

4. **Configure Collaboration Tools**
   - Set up issue templates
   - Configure merge request templates
   - Implement branch protection

5. **Quality Assurance Setup**
   - Configure linting tools
   - Set up automated checks
   - Create review processes

6. **Advanced Features**
   - Implement search functionality
   - Set up version control
   - Configure integrations

## Success Metrics

- **Quality**: All markdown files pass linting checks
- **Consistency**: Uniform formatting across all documents
- **Collaboration**: Active participation from team members
- **Maintenance**: Regular updates and improvements
- **User Experience**: Easy navigation and search functionality

## Maintenance Guidelines

- Regular review of documentation quality
- Update templates based on feedback
- Monitor and improve CI/CD pipeline
- Keep dependencies and tools updated
- Gather and act on user feedback

Remember: The goal is to create a repository that makes it easy for anyone to contribute high-quality markdown documentation while maintaining consistency and professional standards.