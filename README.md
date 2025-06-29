# 🔥 LLM-Powered Dataset Generator

An intelligent dataset generator that uses Large Language Models to create custom structured datasets from natural language descriptions. Simply describe your dataset requirements in plain English, and let AI generate realistic sample data for you!

## ✨ Features

- **Natural Language Input**: Describe your dataset in plain English
- **Intelligent Schema Generation**: LLM automatically creates appropriate column types and constraints
- **Excel-like Data Types**: Supports integers, floats, text, dates, categories, and booleans
- **Smart Constraint Detection**: Automatically applies reasonable constraints based on column names
- **Multiple Export Formats**: Save as CSV, Excel (.xlsx), or JSON
- **Flexible Architecture**: Works with various Hugging Face models
- **Memory Efficient**: Uses 4-bit quantization for large models

## 🚀 Quick Start

### Prerequisites

```bash
pip install transformers torch pandas openpyxl bitsandbytes accelerate
```

### Basic Usage

```python
from dataset_generator import generate_dataset_spec, generate_sample_data

# Describe your dataset
user_desc = "Customer data with ID, Name, Email, Age (18-65), City, and Registration Date"

# Generate schema
spec = generate_dataset_spec(user_desc)

# Create sample data
df = generate_sample_data(spec, num_rows=100)

# Save dataset
df.to_csv("customers.csv", index=False)
```

## 📊 Supported Data Types

| Type | Description | Example Use Cases |
|------|-------------|-------------------|
| `integer` | Whole numbers with optional min/max | IDs, counts, ages, quantities |
| `float` | Decimal numbers with ranges | Prices, ratings, percentages |
| `text` | String data with optional categories | Names, descriptions, addresses |
| `date` | Date values (YYYY-MM-DD) | Birth dates, registration dates |
| `datetime` | Date and time stamps | Transaction timestamps, logs |
| `boolean` | True/False values | Active status, preferences |
| `category` | Predefined options | Departments, product types, ratings |

## 🎯 Example Use Cases

### 1. E-commerce Dataset
```python
user_desc = "Product catalog with ProductID, Name, Category, Price (10-500), Stock (0-1000), Rating (1-5), InStock (boolean)"
```

### 2. Employee Database
```python
user_desc = "Employee records with ID, FirstName, LastName, Department, Salary (30000-120000), HireDate, IsActive"
```

### 3. Survey Responses
```python
user_desc = "Customer feedback with ResponseID, CustomerAge (18-70), Satisfaction (1-5), Comments, SurveyDate"
```

### 4. Financial Transactions
```python
user_desc = "Transaction log with TransactionID, Amount (1-10000), Currency, Date, Status, PaymentMethod"
```

## 🔧 Configuration

### Model Selection
The generator supports various Hugging Face models. Default is `Qwen/Qwen2.5-3B`:

```python
model_name = "Qwen/Qwen2.5-3B"  # Fast and efficient
# model_name = "microsoft/DialoGPT-large"  # Alternative option
# model_name = "google/flan-t5-base"  # For lighter setups
```

### Quantization Settings
Optimized for memory efficiency:
```python
quant_config = BitsAndBytesConfig(
    load_in_4bit=True,
    bnb_4bit_use_double_quant=True,
    bnb_4bit_compute_dtype=torch.bfloat16,
    bnb_4bit_quant_type="nf4"
)
```

## 📁 Project Structure

```
llm-dataset-generator/
├── dataset_generator.py    # Main generator script
├── examples/              # Example datasets and usage
├── requirements.txt       # Python dependencies
├── README.md             # This file
└── datasets/             # Generated sample datasets
```

## 🛠️ Advanced Usage

### Custom Constraints
```python
# Manual constraint override
spec = {
    "dataset_name": "Custom Dataset",
    "columns": [
        {
            "name": "ProductName",
            "type": "text",
            "constraints": {
                "categories": ["Laptop", "Phone", "Tablet", "Monitor"]
            }
        }
    ]
}
```

### Batch Generation
```python
# Generate multiple related datasets
datasets = [
    "Customer data with ID, Name, Email, Phone",
    "Order data with OrderID, CustomerID, Product, Amount, Date",
    "Product data with ProductID, Name, Category, Price, Stock"
]

for desc in datasets:
    spec = generate_dataset_spec(desc)
    df = generate_sample_data(spec, num_rows=50)
    # Process each dataset...
```

## 📈 Performance

- **Memory Usage**: ~2-4GB with 4-bit quantization
- **Generation Speed**: ~1-5 seconds per schema
- **Data Creation**: ~100-1000 rows per second
- **Supported Models**: Any Hugging Face causal LM

## 🤝 Contributing

Contributions are welcome! Here are some ways you can help:

- 🐛 Report bugs and issues
- 💡 Suggest new features or data types
- 📚 Improve documentation
- 🧪 Add more example datasets
- 🔧 Optimize performance

### Development Setup
```bash
git clone https://github.com/Atharvax16/llm-dataset-generator.git
cd llm-dataset-generator
pip install -r requirements.txt
python dataset_generator.py
```

## 📋 Roadmap

- [ ] Support for relational datasets (foreign keys)
- [ ] Time series data generation
- [ ] Custom business logic rules
- [ ] Web interface for non-technical users
- [ ] Integration with popular ML frameworks
- [ ] Real-world distribution patterns
- [ ] Multi-language support

## ⚠️ Limitations

- Generated data follows simple statistical patterns
- No complex relationships between columns
- Limited to tabular/structured data
- Requires GPU for optimal performance
- Quality depends on the underlying LLM

## 🙏 Acknowledgments

- [Hugging Face Transformers](https://github.com/huggingface/transformers) for the LLM infrastructure
- [BitsAndBytes](https://github.com/TimDettmers/bitsandbytes) for efficient quantization
- [Pandas](https://pandas.pydata.org/) for data manipulation

## 📞 Support

- 📧 Email: atharvakocharekar0@gmail.com
- 🐛 Issues: [GitHub Issues](https://github.com/Atharvax16/llm-dataset-generator/issues)
- 💬 Discussions: [GitHub Discussions](https://github.com/Atharvax16/llm-dataset-generator/discussions)

---

⭐ **Star this repo if you find it useful!** ⭐

Made with ❤️ by [Atharvaxx]
