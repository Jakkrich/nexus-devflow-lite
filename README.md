# Nexus DevFlow Lite

Nexus DevFlow Lite คือชุด agent skills สำหรับช่วยทำงานพัฒนา software แบบ Markdown-first ตั้งแต่คุย idea, แตก task, วางแผน, build, verify, test, debug, review ไปจนถึงสรุป commit

เหมาะกับทีมที่อยากให้ AI ทำงานเป็นขั้นตอน มีหลักฐานตรวจสอบได้ และไม่อยากพึ่ง JSON, dashboard หรือ CLI เฉพาะทาง

## ติดตั้ง

ติดตั้งทั้งชุด:

```bash
npx skills add Jakkrich/nexus-devflow-lite
```

ติดตั้งเฉพาะ skill เดียว:

```bash
npx skills add Jakkrich/nexus-devflow-lite --skill devflow-task
```

หลังติดตั้งแล้ว ให้เรียกชื่อ skill ใน prompt ได้โดยตรง เช่น:

```text
devflow-feature ช่วยแตก idea ระบบ team invite
devflow-task 001 Add team invite flow
devflow-plan 001
devflow-build 001
devflow-verify 001
```

## ใช้งานแบบไหนดี

Flow หลักที่แนะนำ:

```text
devflow-feature -> devflow-task -> devflow-plan -> devflow-build -> devflow-verify
```

ตัวอย่าง:

```text
devflow-feature อยากเพิ่มระบบ authentication lockout
devflow-task 001 Add authentication lockout
devflow-plan 001
# ตรวจ plan.md แล้ว approve ก่อน
devflow-build 001
devflow-verify 001
```

สำหรับงานเสริม ให้เรียก skill เฉพาะทางตามสถานการณ์ เช่น `devflow-test`, `devflow-debug`, `devflow-review`, `devflow-security` หรือ `devflow-database`

## รายการ Skill

| Skill | ทำอะไร | ใช้เมื่อไหร่ |
| --- | --- | --- |
| `devflow-feature` | คุยและสกัด feature idea ให้ชัดก่อนแตกเป็น task | idea ยังหลวม มี requirement, risk หรือ edge case ที่ต้องคุยเพิ่ม |
| `devflow-task` | สร้าง task workspace พร้อม `spec.md` และ `task_log.md` | feature หรือ bug ถูกนิยามพอจะเริ่มเป็น task แล้ว |
| `devflow-plan` | สร้าง `plan.md` พร้อม subtasks, test decisions และ approval gate | ต้องการแผน implementation ก่อนให้ AI แก้ code |
| `devflow-build` | implement ตาม `plan.md` ที่ approved แล้วทีละ subtask | แผนผ่านแล้ว และพร้อมให้ AI ลงมือแก้ code |
| `devflow-verify` | ตรวจงานและสร้าง `qa_report.md` พร้อม evidence และ pass/fail verdict | build เสร็จแล้ว ต้องการตรวจว่าตรง spec จริงไหม |
| `devflow-test` | วางหรือรัน focused test strategy และสร้าง `test_report.md` | อยากรู้ว่าควร test อะไร หรือ test ที่มีพอไหม |
| `devflow-debug` | วิเคราะห์ failure และสร้าง `debug_report.md` | test fail, behavior แปลก หรือยังไม่รู้ root cause |
| `devflow-review` | review plan, code, PR หรือ task แล้วสร้าง `review_report.md` | ต้องการ second opinion ก่อน merge หรือก่อนเดินหน้าต่อ |
| `devflow-commit` | สรุปงานที่ verify แล้วเป็น `commit_summary.md` และเสนอ commit message | ก่อน commit งานที่ทำเสร็จ |
| `devflow-frontend` | ช่วยคิดเรื่อง UI, UX, browser behavior, responsive และ accessibility | งานกระทบ frontend หรือ user flow |
| `devflow-backend` | ช่วยคิดเรื่อง API, service, auth, error handling และ backend design | งานกระทบ backend หรือ service contract |
| `devflow-database` | ช่วยคิดเรื่อง schema, migration, index และ data integrity | งานกระทบ database หรือข้อมูลถาวร |
| `devflow-security` | ช่วยตรวจ auth, permission, token, validation และ abuse risk | งานมี security หรือ permission risk |
| `devflow-prd` | สร้าง `prd.md` สำหรับ initiative ที่ใหญ่กว่า feature เดียว | เรื่องใหญ่ ต้องคุย product direction ก่อนแตก task |
| `devflow-research` | สร้าง `research.md` จากการสำรวจ codebase หรือข้อมูลอ้างอิง | ต้องเข้าใจระบบเดิมก่อนวางแผน |
| `devflow-wiki` | สร้าง `wiki_note.md` สำหรับเก็บความรู้ที่ควรใช้ซ้ำ | มี convention หรือ decision ที่ควรจำไว้ |
| `devflow-changelog` | สร้าง `changelog_entry.md` หลังงานผ่าน verification | ต้องการข้อความ changelog จากงานที่เสร็จ |
| `devflow-insight` | สร้าง `insight.md` จากบทเรียนของงานหรือ bug | อยากสรุปสิ่งที่เรียนรู้ไว้ใช้ต่อ |

## Artifact ที่จะได้

สำหรับ task ทั่วไป:

```text
.workspaces/specs/{ID}-{slug}/
  spec.md
  plan.md
  task_log.md
  qa_report.md
```

สำหรับ feature discovery:

```text
.workspaces/features/{slug}/
  feature_brief.md
```

skill อื่นอาจสร้างไฟล์รายงานเพิ่มเติมตามงาน เช่น:

```text
test_report.md
debug_report.md
review_report.md
commit_summary.md
prd.md
research.md
wiki_note.md
changelog_entry.md
insight.md
```

## กติกาสำคัญ

- ใช้ Markdown เป็น artifact หลัก
- ไม่มี JSON artifacts
- ไม่มี dashboard
- ไม่ต้องใช้ CLI เฉพาะของ Nexus DevFlow
- `devflow-task` และ `devflow-plan` ไม่ควรแก้ source code
- `devflow-build` ต้องรอให้ `plan.md` ถูก approve ก่อน
- `devflow-verify` ต้องมี evidence จริงก่อนให้ verdict เป็น pass

## ตัวอย่าง Prompt

เริ่มจาก feature idea:

```text
devflow-feature อยากเพิ่มระบบ invite สมาชิกเข้าทีม ช่วยถาม requirement และ risk ที่ควรคิดก่อน
```

แตกเป็น task:

```text
devflow-task 001 Add team invite flow
```

วางแผนก่อน build:

```text
devflow-plan 001
```

เริ่ม build หลัง approve:

```text
devflow-build 001
```

ตรวจงาน:

```text
devflow-verify 001
```
