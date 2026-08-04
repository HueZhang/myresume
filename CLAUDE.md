# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository overview

This is a personal resume and interview preparation document repository. It contains markdown resumes for multiple tech stacks (.NET, Java, WPF), interview Q&A documents organized by topic, and job requirement notes. All markdown files are also exported to PDF under `pdf/`.

## Key documents

- `java_resume.md` — Primary Java resume (currently maintained)
- `wpf_resume.md` — WPF resume variant
- `dotnet_resume.md` — .NET resume variant
- `dotnet_resume_old.md` — Previous .NET resume (reference for detailed project descriptions)
- `java_qa.md` — Java interview Q&A organized by topic (merged: JVM, interview.txt 朋友面经, java_project_qa, project 讲稿)
- `dotnet_qa.md` — .NET interview Q&A (merged from dotnet_resume_interview_qa / interview_qa / resume_interview_qa)
- `wpf_qa.md` — WPF + WinForms desktop interview Q&A (merged)
- `frontend_vue3_qa.md` — Vue3 full-stack interview Q&A (merged from two frontend docs)
- `db_interview_qa.md` / `database_project_qa.md` — language-agnostic DB/common Q&A (kept separate, not merged)
- `erp_interview_qa.md` / `mes_interview_qa.md` / `upper_computer_interview_qa.md` / `common_industrial_system_qa.md` — industry domain Q&A
- `归档/` — merged-away source files backup (not converted to PDF)
- `tips.md` — Interview tips and strategies
- `prompts/review.md` — Prompt used for MD-to-PDF conversion
- `requirements/` — Job requirements and company research notes

## Tech stack conventions across resume variants

When translating projects between tech stacks, use these mappings:

| .NET | Java |
|------|------|
| C# / .NET Core | Java / Spring Boot |
| ASP.NET Core Web API | Spring MVC / Spring Boot |
| EF Core | MyBatis-Plus |
| Dapper / SqlSugar | MyBatis / JdbcTemplate |
| Refit | Feign (OpenFeign) |
| Workflow Core | Flowable |
| Hangfire | XXL-Job |
| Serilog | Logback / SLF4J |
| ABP / Admin.NET | Spring Security + Sa-Token |
| SignalR | WebSocket / Netty |

## Resume patterns

- Projects are grouped as distributed microservice systems using Spring Cloud Alibaba (Nacos for registration/config, Spring Cloud Gateway for API gateway, Feign for inter-service calls)
- Each microservice system has a shared API gateway handling JWT auth, then downstream services doing RBAC authorization
- Multi-tenant data isolation uses MyBatis-Plus interceptors that read tenant ID from gateway-forwarded headers
- Sub-services within a parent project do NOT list their tech stack in titles — the parent project title carries the stack identifier

## Interview Q&A document structure

`java_qa.md` is organized into numbered Q-sections with a quick-index table at the bottom. When adding new questions, append to the appropriate section and update the index table. The document uses a consistent format:

- `## 分组标题 (roman numeral)`
- `### Q{number}: 问题标题`
- Code blocks use language-annotated fences
- Comparison tables for contrasting approaches
- "延伸" (extension) subsections for related knowledge

## Markdown-to-PDF conversion

PDF files in `pdf/` are generated from markdown sources using the prompt defined in `prompts/review.md`. Do not modify PDF files directly — edit the markdown source and re-generate. The workflow converts **only root-level `*.md` files**; files under subdirectories (e.g. `归档/`) are explicitly skipped.
