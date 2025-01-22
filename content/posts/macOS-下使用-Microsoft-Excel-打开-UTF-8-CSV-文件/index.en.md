---
title: Opening UTF-8 CSV Files with Microsoft Excel on macOS
date: 2018-01-26T01:25:40+08:00
tags:
  - Technology
  - Excel
  - CSV
  - utf8
slug: opening-utf8-csv-files-with-microsoft-excel-on-macos
---

Microsoft Excel on macOS doesn't provide a direct way to set character encoding when opening files. This makes it challenging to properly open UTF-8 encoded CSV files. However, there's a workaround using Excel's `Get External Data` feature that allows you to successfully open UTF-8 CSV files.

<!--more-->

## Steps

1. Create a new blank Excel workbook
2. Navigate to the `Data` tab and select `Get External Data > Import Text File...`

![import text file](./Screenshot_1.png)

3. Locate and select your CSV file. In the import wizard, choose `Unicode (UTF-8)` as the file origin, then click Next.

![choose charset](./Screenshot_2.png)

4. In the next screen, select your desired delimiter options, then click Finish.

![choose delimiter](./Screenshot_3.png)

That's it! Your UTF-8 CSV file should now be properly imported with all characters displaying correctly.
