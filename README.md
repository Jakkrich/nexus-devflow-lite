# Nexus DevFlow Lite

ชุด workflow ของ DevFlow แบบ Markdown-first ที่แพ็กเป็น agent skills สำหรับติดตั้งใช้งานได้ทันที

นี่คือเวอร์ชันเบาของ Nexus-DevFlow:

- ไม่มี JSON artifacts
- ไม่มี dashboard
- ไม่ผูกกับ CLI
- ไม่ copy agent library ทั้งชุด

ติดตั้งจาก repo นี้:

```bash
npx skills add Jakkrich/nexus-devflow-lite
```

ติดตั้งเฉพาะ skill เดียว:

```bash
npx skills add Jakkrich/nexus-devflow-lite --skill devflow-task
```

## รายการ Skill

ทุก skill ในชุดนี้พร้อมใช้งานแล้ว

| Skill | ทำอะไร | ใช้เมื่อไหร่ |
| --- | --- | --- |
| `devflow-feature` | เปลี่ยน feature idea ให้เป็น `feature_brief.md` ที่ชัดและโฟกัส | "อยากมี team invites แต่ flow กับ edge cases ยังไม่ชัด" |
| `devflow-task` | สร้าง task workspace พร้อม `spec.md` และ `task_log.md` | "เอา feature ที่ตกลงแล้วมาแตกเป็น task ที่ทำงานต่อได้" |
| `devflow-plan` | สร้าง `plan.md` พร้อม phases, subtasks, test decisions และ approval gate | "วางแผน task 001 ก่อนเริ่ม coding" |
| `devflow-build` | implement plan ที่ approved แล้วทีละ subtask | "เริ่ม build subtask แรกหลังจาก approve plan แล้ว" |
| `devflow-verify` | สร้าง `qa_report.md` พร้อม evidence และ verdict แบบ pass/fail | "ตรวจว่าที่ implement ตรงตาม task จริงไหม" |
| `devflow-test` | สร้างหรือรัน focused test strategy และ `test_report.md` | "task นี้ยังขาด test อะไรบ้าง" |
| `devflow-debug` | สร้าง `debug_report.md` สำหรับ failure และ root-cause investigation | "test นี้ fail ช่วยหา cause จริง" |
| `devflow-review` | สร้าง `review_report.md` สำหรับ plan, code, PR หรือ task | "review change นี้ก่อน merge" |
| `devflow-commit` | สร้าง `commit_summary.md` และเสนอ commit message | "สรุปงานที่ verify แล้วเพื่อ commit" |
| `devflow-frontend` | ช่วยตัดสินใจเรื่อง UI, browser, accessibility และ frontend implementation | "review form flow และ responsive behavior" |
| `devflow-backend` | ช่วยตัดสินใจเรื่อง API, service, auth และ backend implementation | "ออกแบบ endpoint และ error contract" |
| `devflow-database` | ช่วยตัดสินใจเรื่อง schema, migration, index และ data integrity | "feature นี้ควรเพิ่ม table, index หรือ migration ไหม" |
| `devflow-security` | ช่วยตัดสินใจเรื่อง auth, permissions, token, validation และ abuse risk | "ตรวจ invite tokens, rate limits หรือ permission risks" |
| `devflow-prd` | สร้าง `prd.md` สำหรับ product initiative ที่ใหญ่กว่า feature เดียว | "เรื่องนี้ใหญ่กว่า feature เดียว ควรเขียน PRD ก่อน" |
| `devflow-research` | สร้าง `research.md` สำหรับ research โค้ดหรือข้อมูลภายนอก | "สำรวจ pattern เดิมใน codebase ก่อนวางแผน" |
| `devflow-wiki` | สร้าง `wiki_note.md` สำหรับเก็บ project knowledge ที่ใช้ซ้ำได้ | "เก็บ convention ที่ verify แล้วไว้ใช้ใน task ถัดไป" |
| `devflow-changelog` | สร้าง `changelog_entry.md` หลังงานผ่าน verification | "ร่าง changelog จาก task ที่เสร็จแล้ว" |
| `devflow-insight` | สร้าง `insight.md` จากงานที่สำเร็จหรือล้มเหลว | "ดึงบทเรียนจาก task หรือ bug นี้" |

ผลการ dry-run:

- `devflow-feature`: เพิ่มเป็น lightweight discovery step ก่อน task intake
- `devflow-task`: สร้าง Markdown task artifacts ได้
- `devflow-plan`: สร้าง `plan.md` พร้อม `Approval: Pending` ได้
- `devflow-build`: หยุดถูกต้องเมื่อ approval ยัง pending
- `devflow-build`: เริ่ม approved build path และสร้าง expected failing tests สำหรับ subtask แรกได้
- `devflow-verify`: สร้าง `qa_report.md` แบบผ่านหลัง build เสร็จได้
- Phase 3-5 skills ถูกทดลองรวมใน overall dry-run แล้ว

## รูปแบบ Artifact

Task artifacts จะอยู่ใน target project:

```text
.workspaces/specs/{ID}-{slug}/
  spec.md
  plan.md
  task_log.md
  qa_report.md
```

Feature discovery artifacts จะอยู่ใน:

```text
.workspaces/features/{slug}/
  feature_brief.md
```

## Workflow การใช้งาน

```text
devflow-feature -> feature discovery before task intake
devflow-task   -> task intake
devflow-plan   -> implementation plan
devflow-build  -> approved implementation
devflow-verify -> verification report
devflow-test   -> focused test strategy/report
devflow-debug  -> root-cause report
devflow-review -> review report
devflow-commit -> commit summary
```

ตัวอย่าง flow ปกติ:

```text
devflow-feature Add authentication lockout
devflow-task 001 Add authentication lockout
devflow-plan 001
# user reviews plan.md and approves it
devflow-build 001
devflow-verify 001
```

## กติกา

- Markdown-first
- ไม่มี JSON artifacts
- ไม่มี dashboard
- ไม่ผูกกับ CLI
- ห้ามแก้ source code ระหว่าง `devflow-task` หรือ `devflow-plan`
- `devflow-build` ต้องมี approval status ใน `plan.md` เป็น `Approved`
- `devflow-verify` ต้องมี evidence จริงก่อนให้ verdict เป็น pass

## โครงสร้าง Repo

```text
skills/
  _shared/
    references/devflow-conventions.md
  devflow-feature/
    SKILL.md
    references/templates/feature_brief.template.md
  devflow-task/
    SKILL.md
    references/templates/spec.template.md
    references/templates/task_log.template.md
  devflow-plan/
    SKILL.md
    references/agents/planner.md
    references/templates/plan.template.md
  devflow-build/
    SKILL.md
    references/agents/coder.md
  devflow-verify/
    SKILL.md
    references/agents/reviewer.md
    references/templates/qa_report.template.md
  devflow-test/
  devflow-debug/
  devflow-review/
  devflow-commit/
  devflow-frontend/
  devflow-backend/
  devflow-database/
  devflow-security/
  devflow-prd/
  devflow-research/
  devflow-wiki/
  devflow-changelog/
  devflow-insight/
```

## งานถัดไป

step ถัดไปที่แนะนำ:

1. ทดลอง approved build path จนถึง implementation จริง
2. Dry-run `devflow-verify` หลัง build เสร็จสมบูรณ์
3. Dry-run Phase 3-5 skills กับตัวอย่างเดียวแบบ end-to-end

## devflow-feature

`devflow-feature` คือ discovery skill ที่ใช้ก่อน `devflow-task`

เป้าหมาย:

- ดึง requirement ที่ยังซ่อนอยู่จากผู้ใช้ด้วย interaction สั้น ๆ
- คุย feasibility, risks และ alternatives ก่อนสร้าง task
- เปลี่ยน feature idea ที่ยังหลวมให้เป็น feature brief ที่กระชับ
- แนะนำว่าควรไปต่อที่ `devflow-task` หรือยัง

Artifact ที่แนะนำ:

```text
.workspaces/features/{slug}/
  feature_brief.md
```

Flow ที่แนะนำ:

```text
devflow-feature Add team invite flow
devflow-task 001 Add team invite flow
devflow-plan 001
devflow-build 001
devflow-verify 001
```
