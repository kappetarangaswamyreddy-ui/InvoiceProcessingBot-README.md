
> **Tip:** In some setups, `Data/` is used instead of `Config/`. Both are supported—just update `in_ConfigFile` in `Main.xaml`.

## ⚙️ Config.xlsx (Settings sheet)
| Name                | Example Value                         | Notes |
|---------------------|---------------------------------------|------|
| InputFolder         | `Input` or `Data\Input`               | Folder with PDFs |
| OutputProcessedFile | `Output\Invoices_Processed.xlsx`      | Valid invoices |
| OutputErrorFile     | `Output\Invoices_Errors.xlsx`         | Invalid invoices |
| SuccessFolder       | `Archive\Success`                     | Archive OK |
| FailedFolder        | `Archive\Failed`                      | Archive bad |
| InvoiceFilePattern  | `*.pdf`                               | PDF filter |

## 🚀 How to run
1. Open the solution in **UiPath Studio** (REFramework template).
2. In `Main.xaml` → set `in_ConfigFile` default to `Data\Config.xlsx`.
3. I drop 10 sample PDFs into **Input**.
4. **Run**. Watch Output panel for logs.

## ✅ Validation rules (sample)
- VendorName, InvoiceNumber, InvoiceDate, TotalAmount are required.
- TotalAmount must be > 0.
- If any required field missing → row goes to **Errors** and PDF → `Archive/Failed`.

## 🧪 Test data
- You can generate dummy invoices or use the included samples (`/Input`).
- For OCR variance, use mixed fonts or lightly noisy scans.

## 🛠️ Troubleshooting
- **“Folder does not exist”**: ensure `Input/Output/Archive` match `Config.xlsx`.
- **Excel lock errors**: don’t mix Classic Workbook inside **Use Excel File**; keep to Modern Excel activities.
- **Move File error**: ensure Move File is **outside** `Use Excel File` scope; verify `Archive/…` folders exist.
- **Path is null**: ensure `in_TransactionItem` is mapped and `Read PDF with OCR` FileName = `in_TransactionItem`.

## 🗺️ Roadmap
- **v2:** Orchestrator **Queues** (Dispatcher/Performer pattern)
- **v3:** **API** push into ERP/Accounting system
- **v4:** **AI Center** skill for smarter field extraction
- **v5:** DU **ML Extractor**, human validation station, confidence thresholds

## 🗣️ Interview crib notes
- “Each transaction = single PDF; **Config-driven** paths; OCR + Regex; **validation layer**; Excel append; **archive policy**; handled business vs system exceptions within **REFramework**.”

## 📷 Screenshots (add yours)
- `docs/flow-overview.png`
- `docs/reframework-states.png`
- `docs/output-excel.png`

## 📄 License
MIT — free to use and adapt. See `LICENSE`.
