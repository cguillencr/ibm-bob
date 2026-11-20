# Role handoffs and gates

| From | To | Contract | Gate |
|---|---|---|---|
| Analyst | Developer | Approved spec + resolved blocking decisions | Human specification approval |
| Developer | QA | Diff + test evidence + draft PR | Human code review |
| QA | SRE | Acceptance and regression results | Release authorization |
| Support | SRE | Sanitized diagnostic bundle | Authorized access |
| SRE | Developer | RCA + fix proposal + observability changes | Change approval |

A mode is a role configuration, **not** proof of autonomous orchestration. Users may switch modes manually; automated handoff is future research subject to verified Bob capabilities.

A blocked spec must not be implemented without explicit exception. An unanswered nonblocking question may remain open if the risk is documented and accepted.


## Portability across technology stacks

The SDLC workflows and artifact handoffs are designed to stay stable across projects. Domain-specific skills (for example, IBM watsonx Orchestrate ADK skills) should be installed **in each target project where required**, not baked into the generic foundation. See [Project specialization](project-specialization.md).
