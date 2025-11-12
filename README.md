# End-to-End Invoice Processing Bot (UiPath)

**Tech:** UiPath **REFramework**, **PDF/OCR**, **Regex extraction**, Excel Append, Config-driven paths, robust logging & archiving.  
**Flow:** Read invoice PDFs → OCR → extract fields → validate → write to Excel → archive Success/Failed.

## 🎯 What this bot does
- Loops through all PDFs in the **Input** folder (each file = 1 transaction).
- Uses **Read PDF with OCR** + **Regex** to extract:
  - VendorName, InvoiceNumber, InvoiceDate, Subtotal, Tax, TotalAmount
- Validates required fields and amounts.
- Appends valid rows to `Invoices_Processed.xlsx`; writes errors to `Invoices_Errors.xlsx`.
- Moves each PDF to `Archive/Success` or `Archive/Failed`.

## 🧱 Architecture (REFramework mapping)
- **Init:** load `Config.xlsx`, collect file list, create folders if missing.
- **GetTransactionData:** map `TransactionNumber → file path` (TransactionItem).
- **Process:** OCR → Regex → validate → write Excel → move PDF.
- **End:** summary logs (ready to extend with email/slack).

## 📁 Folder structure
