## ⚙️ My Configuration Setup (Config.xlsx)

For this project, I created a centralized **Config.xlsx** file to control all input, output, and archive paths dynamically.  
This helps the bot stay flexible and portable — I can move the entire folder anywhere, and the automation still works without hardcoded paths.

| Name | Example Value | Description |
|------|----------------|-------------|
| InputFolder | `Data\Input` | Folder where invoice PDFs are stored |
| OutputProcessedFile | `Data\Output\Invoices_Processed.xlsx` | File where valid invoices are written |
| OutputErrorFile | `Data\Output\Invoices_Errors.xlsx` | File where invalid invoices are written |
| SuccessFolder | `Data\Archive\Success` | Folder for successfully processed PDFs |
| FailedFolder | `Data\Archive\Failed` | Folder for failed or incomplete PDFs |
| InvoiceFilePattern | `*.pdf` | Used to pick all invoice files from Input |

---

## 🚀 How I Built & Run This Bot

I developed this automation using **UiPath REFramework** from scratch.  
Each transaction represents a single invoice PDF.

1. Opened the project in **UiPath Studio** (based on the REFramework template).  
2. Set the `in_ConfigFile` argument in **Main.xaml** to point to my Config file (`Data\Config.xlsx`).  
3. Added 10 sample invoices inside the **Input** folder.  
4. Clicked **Run** — the bot automatically:
   - Reads each PDF using **Read PDF with OCR**.  
   - Extracts key fields with **Regex** (VendorName, InvoiceNo, Date, Subtotal, Tax, Total).  
   - Validates all mandatory fields.  
   - Appends clean data into **Invoices_Processed.xlsx**.  
   - Logs invalid invoices into **Invoices_Errors.xlsx**.  
   - Moves each file into the correct **Archive** folder (Success/Failed).  

Everything (paths, patterns, file names) is **Config-driven**, so there’s zero hardcoding.

---

## ✅ My Validation Rules

During processing, the bot applies simple but strong validation to ensure data accuracy:

- **VendorName**, **InvoiceNumber**, **InvoiceDate**, and **TotalAmount** are mandatory.  
- **TotalAmount** must be greater than 0.  
- Missing or invalid data moves the file to **Archive/Failed** and logs the reason in **Invoices_Errors.xlsx**.  
- Valid invoices go to **Archive/Success** and are appended in **Invoices_Processed.xlsx**.

---

## 🧪 My Test Data Setup

I used 10 sample invoice PDFs — a mix of:
- Text-based and scanned invoices (to test OCR reliability).  
- Different vendors and formats.  
- A few intentionally incomplete invoices to test validation and exception handling.

The goal was to simulate a real-world environment where not every invoice is perfect.

---

## 🛠️ Challenges I Solved

While creating this end-to-end automation, I encountered and fixed several real issues:

| Issue | Cause | My Solution |
|-------|--------|-------------|
| **Folder does not exist** | Folder path didn’t match Config.xlsx | Created missing folders manually and verified Config values |
| **Excel file locked** | Used Workbook activity inside Modern Excel scope | Switched fully to **Modern Excel** activities |
| **Move File error** | File was still open when moving | Moved PDF **outside** the Excel scope |
| **Null path in OCR** | Argument not mapped correctly | Mapped `in_TransactionItem` properly in Main.xaml |

Each fix taught me how to handle exceptions gracefully and design resilient UiPath workflows.

---

## 🗺️ Future Enhancements

In the next version, I plan to extend this automation with:
- **Orchestrator Queues (Dispatcher/Performer)** for large-scale processing.  
- **API integration** to push invoice data into accounting systems.  
- **AI Center / ML Extractor** for smart, layout-independent field detection.  
- **Email or Teams notifications** after each batch run.  

---

## 🗣️ My Personal Project Summary

> “I personally developed this End-to-End Invoice Processing Bot using UiPath REFramework.  
> It automates reading invoice PDFs, extracting data with OCR and Regex, validating information, and organizing outputs into structured Excel sheets.  
> I implemented Config-driven architecture, error handling, logging, and auto-archiving to make it production-ready.  
> This project demonstrates my understanding of **RPA development**, **REFramework**, **Document Understanding**, and **end-to-end process automation**.”

---

## 📄 License

This project is licensed under the **MIT License** — free to use, modify, and share for learning or portfolio purposes.
