<div align="center">
    <div align="center">
    <h1><b><i>RapidOCR 📄 PDF</i></b></h1>
    </div>

<a href=""><img src="https://img.shields.io/badge/Python->=3.6,<3.12-aff.svg"></a>
<a href=""><img src="https://img.shields.io/badge/OS-Linux%2C%20Win%2C%20Mac-pink.svg"></a>
<a href="https://pypi.org/project/rapidocr-pdf/"><img alt="PyPI" src="https://img.shields.io/pypi/v/rapidocr-pdf"></a>
<a href="https://pepy.tech/project/rapidocr-pdf"><img src="https://static.pepy.tech/personalized-badge/rapidocr-pdf?period=total&units=abbreviation&left_color=grey&right_color=blue&left_text=Downloads"></a>
<a href="https://semver.org/"><img alt="SemVer2.0" src="https://img.shields.io/badge/SemVer-2.0-brightgreen"></a>
<a href="https://github.com/psf/black"><img src="https://img.shields.io/badge/code%20style-black-000000.svg"></a>
<a href="https://choosealicense.com/licenses/apache-2.0/"><img alt="GitHub" src="https://img.shields.io/github/license/RapidAI/RapidOCRPDF"></a>

</div>

### 简介
本仓库依托于[RapidOCR](https://github.com/RapidAI/RapidOCR)仓库，快速提取PDF中文字，包括扫描版PDF、加密版PDF、可直接复制文字版PDF。

如果是扫描版PDF，暂时不支持版式还原，后续有空会考虑加上，日期不定。

### 整体流程
```mermaid
flowchart LR

A(PDF) --> B{是否可以直接提取内容} --是--> C(PyMuPDF)
B --否--> D(RapidOCR)

C & D --> E(结果)
```

### TODO
- [ ] 支持图像的提取
- [ ] 整合版面分析模型，段落化输出PDF内容
- [ ] 完善仓库文档

### 安装
```bash
# 基于rapidocr_onnxruntime
pip install rapidocr_pdf[onnxruntime]

# 基于rapidocr_openvino
pip install rapidocr_pdf[openvino]
```

### 使用
脚本使用
```python
from rapidocr_pdf import PDFExtracter

pdf_extracter = PDFExtracter()

pdf_path = 'tests/test_files/direct_and_image.pdf'
texts = pdf_extracter(pdf_path)
print(texts)
```

命令行使用
```bash
rapidocr_pdf -path tests/test_files/direct_and_image.pdf
```

### 输入输出说明
**输入**：`Union[str, Path, bytes]`

**输出**：`List` \[**页码**, **文本内容**, **置信度**\]， 具体参见下例：
```python
[
    ['0', '人之初，性本善。性相近，习相远。', '0.8969868'],
    ['1', 'Men at their birth, are naturally good.', '0.8969868'],
]
```

### 更新日志
2023-08-28 v0.0.6 update:
- 解决PyMuPDF版本依赖问题，对应[issue #2](https://github.com/RapidAI/RapidOCRPDF/issues/2)

2023-04-17 v0.0.2 update:
- 完善使用文档
