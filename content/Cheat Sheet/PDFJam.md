---
title: PDFJam Cheat Sheet
---
## Commands

**Merge PDFs**
```bash
pdfjam file1.pdf file2.pdf --outfile output.pdf
```

**Arrange Pages in a Grid**
```bash
pdfjam --nup 2x2 input.pdf --outfile output.pdf
```

**Rotate Pages**
```bash
pdfjam input.pdf --rotate 90 --outfile rotated.pdf
```

**Scale Pages**
```bash
pdfjam input.pdf --scale 0.95 --outfile scaled.pdf
```

**Offset Pages**
```bash
pdfjam input.pdf --offset "1cm 2cm" --outfile offset.pdf
```

**Trim Borders**
```bash
pdfjam input.pdf --trim "1cm 1cm 1cm 1cm" --outfile trimmed.pdf
```

**Select Specific Pages**
```bash
pdfjam file1.pdf '{},2-' file2.pdf '10,3-6' --outfile selected_pages.pdf
```

**Reverse Page Order**
```bash
pdfjam input.pdf 'last-1' --suffix reversed --outfile reversed_order.pdf
```

**Convert Paper Size**
```bash
pdfjam input.pdf --a4paper --outfile converted_a4.pdf
```