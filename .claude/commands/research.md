---
description: Execute multiple research tasks in parallel on a given topic, exploring different aspects simultaneously
allowed-tools: task, read, write, grep, glob, websearch, webfetch
argument-hint: <topic or feature to research>
---

# Research Command

I'll conduct comprehensive parallel research on: $ARGUMENTS

## Research Strategy

I'm launching multiple specialized research agents in parallel to explore different dimensions of this topic simultaneously. Each agent will focus on a specific aspect and produce its own research document.

### Research Dimensions

1. **Technical Implementation Research**
   - Exploring different technical approaches and architectures
   - Analyzing code patterns and best practices
   - Investigating framework/library options
   - Performance and scalability considerations

2. **Security & Risk Research**
   - Identifying potential security vulnerabilities
   - Analyzing risk factors and mitigation strategies
   - Compliance and regulatory considerations
   - Data privacy implications

3. **User Experience Research**
   - UI/UX best practices for this feature
   - Accessibility considerations
   - User workflow optimization
   - Error handling and user feedback

4. **Integration & Compatibility Research**
   - System integration requirements
   - API design considerations
   - Backward compatibility analysis
   - Third-party service integrations

5. **Industry Standards Research**
   - Current industry best practices
   - Competitive analysis
   - Emerging trends and future considerations
   - Case studies and real-world implementations

## Execution Plan

I'll use the Task tool to launch these research agents in parallel. Each agent will:
- Conduct independent research using available resources
- Search the codebase for relevant patterns
- Explore web resources and documentation
- Generate a focused research document

After all agents complete their research, I'll:
1. Synthesize the findings into a comprehensive `research-summary.md`
2. Identify common themes and conflicting recommendations
3. Provide a unified recommendation based on all research dimensions

Let me launch the parallel research agents now:

```parallel-execution
# Agent 1: Technical Implementation Research
Task: Research technical approaches for "$ARGUMENTS"
- Explore different implementation patterns
- Compare architectural approaches
- Analyze performance implications
- Document in technical-research.md

# Agent 2: Security Research  
Task: Research security aspects of "$ARGUMENTS"
- Identify security risks
- Analyze attack vectors
- Research mitigation strategies
- Document in security-research.md

# Agent 3: UX Research
Task: Research user experience for "$ARGUMENTS"
- Analyze UX patterns
- Research accessibility requirements
- Explore user workflows
- Document in ux-research.md

# Agent 4: Integration Research
Task: Research integration requirements for "$ARGUMENTS"
- Analyze integration points
- Research API patterns
- Explore compatibility needs
- Document in integration-research.md

# Agent 5: Industry Research
Task: Research industry practices for "$ARGUMENTS"
- Analyze competitor implementations
- Research best practices
- Explore emerging trends
- Document in industry-research.md
```

## Output Structure

Each research document will follow this structure:
- Executive Summary
- Key Findings
- Detailed Analysis
- Recommendations
- References and Resources

The final synthesis document will include:
- Consolidated findings from all research dimensions
- Cross-dimensional insights
- Unified recommendations
- Implementation roadmap
- Risk matrix
- Decision criteria

This parallel research approach ensures comprehensive coverage while minimizing research time through concurrent execution.