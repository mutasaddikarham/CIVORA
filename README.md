# CIVORA

**Calculate Smarter. Design Better. Build the Future.**

CIVORA is built by Er. Md Mutasaddik Arham. It is a local Windows desktop preview for preliminary civil engineering calculations, raster plan calibration, conceptual column grids, project notes, schedules, and exports.

## Start the Windows x64 app

1. Extract the CIVORA Windows x64 release archive to a folder you can write to.
2. Run CIVORA.exe. No .NET installation is required for this self-contained build.
3. Projects, calculation history, and application overrides are kept locally at %LOCALAPPDATA%\CIVORA\civora.db.

The app does not send plans or project data to a server. Basic calculations, drawing operations, persistence, and exports run locally.

## What is implemented

- A dark WPF interface with all 22 navigation routes wired to a working page or calculator.
- An offline, versioned library of 36 illustrative engineering defaults. Entries show category, unit, source, status, assumptions, and editability. Save application overrides separately, restore the built-in values, or save/load editable project values.
- A project workspace backed by SQLite: create, load, rename, duplicate, delete, and save projects; keep calculation history; search history; and export project JSON.
- Raster plan import for PNG, JPG/JPEG, TIFF, BMP, and GIF. The original file is referenced and kept intact.
- Manual scale calibration from two points and a known distance in mm, cm, m, in, or ft; a plan origin; a footprint-based manual workflow; and editable candidate columns that can be added or dragged.
- Conceptual grid generation from a rectangular footprint, a maximum preliminary span, and candidate section dimensions. Each candidate carries a low-confidence/review status and identifies missing design information. This is geometry generation, not plan recognition.
- A synchronized observable column schedule with editable coordinates, sizes, material, notes, review status, candidate reason, span notes, conflict notes, confidence, and missing-information fields. Save it with the project or export CSV.
- Working calculators for scale, unit conversion, geometry and area, concrete quantities, material estimates, structural loads, idealized beam cases, average column stress, concentric footing pressure, reinforcement, brickwork, and surveying. Results show formulas, inputs, steps, assumptions, and limitations; saved calculations appear in local history.
- Annotated PNG overlay, layered ASCII DXF, vector PDF drawing sheet, PDF calculation summary, CSV schedules, and JSON project export.

## Plan workflow

Open AI Plan Analyzer, import a raster plan, select two points on a known dimension, enter the real distance and unit, and apply calibration. Set the drawing origin. For a conceptual layout, enter a rectangular building footprint and maximum preliminary span, then generate a grid or add and drag individual candidates. Review and edit the schedule, then save the project.

The AI Plan Analyzer name describes the intended product area. This preview does not contain an AI model, OCR, computer vision, or automatic architectural-object recognition. The generated grid is based on user-entered rectangular dimensions, not geometry detected from the image.

## Engineering scope and safety

CIVORA does not implement verified BNBC, ACI, or other design-code checks, load combinations, structural member capacity design, or automated safety verification. It does not infer dimensions, floor count, occupancy, loads, or materials from a plan. The default values are examples; confirm project specifications and applicable standards. The software must not be used by itself to approve a design for construction. Have a qualified engineer review all project inputs and outputs.

Current plan-workspace limitations include: PDF page import, OCR and automatic detection, crop/rotate/contrast controls, zoom/pan, geometric conflict detection, alternative layout comparison, column locking/deletion, undo/redo, layer visibility controls, and beam force diagrams are not implemented. Grid generation always replaces the current candidate list. The calibration assumes horizontal/vertical orientation and does not correct image skew. DXF and PDF exports contain vector structural geometry but do not embed the raster architectural background. PNG preserves the visible image overlay.

The app uses a dark theme only. Light theme, accent settings, and configurable keyboard shortcuts are not implemented. The defaults page edits supplied values but does not currently add new material or occupancy records.

## Build and test from source

Install the .NET 10 SDK on Windows. From the CIVORA source folder, the full solution can be built and tested with: dotnet build CIVORA.sln -c Release -m:1 and dotnet test CIVORA.sln -c Release --no-build -m:1. The equivalent project-specific commands are:

    dotnet restore src\Civora.Desktop\Civora.Desktop.csproj
    dotnet build src\Civora.Desktop\Civora.Desktop.csproj -c Release
    dotnet test tests\Civora.Tests\Civora.Tests.csproj -c Release
    dotnet publish src\Civora.Desktop\Civora.Desktop.csproj -c Release -r win-x64 --self-contained true -p:PublishSingleFile=false -p:PublishReadyToRun=true -o release\win-x64

The xUnit suite currently contains 18 tests covering core formulas, input validation, grid coordinates, default loading and overrides, project persistence, and CSV/DXF/PDF exports.

## Technology and licensing

- Presentation: C# 10 / WPF / CommunityToolkit.Mvvm.
- Engineering and persistence: separate .NET library, Microsoft.Data.Sqlite, versioned built-ins and separate local override rows.
- PDF export: QuestPDF 2026.9.1. CIVORA configures the QuestPDF Community License. Users and organizations must check their own eligibility under the [official QuestPDF license selection guide](https://www.questpdf.com/license/guide.html). The guide's current criteria include individuals, qualifying academic/charitable/open-source uses, and small businesses below the stated revenue threshold; public-sector entities and publicly traded companies are excluded from the Community License. A paid license may be required for other production uses.
- DXF export: CIVORA writes a basic ASCII DXF directly; it does not depend on an external CAD SDK.

Generated drawings and preliminary calculations are not stamped engineering documents.



