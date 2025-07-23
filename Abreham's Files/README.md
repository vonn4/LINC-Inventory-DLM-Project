# 📊 Device Lifecycle Management (DLM) Analysis Suite

A comprehensive Python-based tool for analyzing IT inventory data, performing advanced data cleaning, and conducting device lifecycle risk assessments to support strategic technology replacement planning.

## 🎯 **Project Overview**

This suite provides end-to-end device lifecycle management analysis, from raw inventory data cleaning to sophisticated risk-based replacement planning. It handles real-world data quality issues and provides actionable insights for IT management decisions.

## 📁 **Project Structure**

```
📁 DLM Analysis Suite/
├── 📄 Inventory.csv                           # Source inventory data
├── 📄 device_analyzer_with_categories.py     # Main data cleaning & validation tool
├── 📄 device_lifecycle_risk_analyzer.py      # Risk analysis & lifecycle planning tool
├── 📄 README.md                               # This documentation
└── 📄 DLM_Workflow_Diagram.md                # Process workflow diagram
```

## 🔧 **Core Components**

### **1. Device Data Analyzer (`device_analyzer_with_categories.py`)**
- **Primary Function**: Comprehensive data cleaning and validation
- **Input**: Raw inventory CSV file
- **Output**: Cleaned Excel file with multiple analysis sheets

**Key Features:**
- ✅ **Brand Normalization**: Standardizes brand names (HP, Dell, Apple, etc.)
- ✅ **Category Classification**: Validates device categories (Desktop, Laptop, Tablet, etc.)
- ✅ **Purchase Date Validation**: Ensures dates are valid and reasonable (2010-present)
- ✅ **Device Status Analysis**: Categorizes devices as Available/Active vs Unavailable/Inactive
- ✅ **Advanced Data Recovery**: Attempts to recover missing brand/category from description fields
- ✅ **Multi-tier Validation**: Creates progressively cleaner datasets

### **2. Device Lifecycle Risk Analyzer (`device_lifecycle_risk_analyzer.py`)**
- **Primary Function**: Risk-based lifecycle management analysis
- **Input**: Cleaned data from analyzer (Analysis_Ready_Data sheet)
- **Output**: Risk-categorized Excel file with replacement recommendations

**Risk Scoring System:**
- 🕐 **Device Age (50 points max)**: 5+ years = High, 3-5 years = Medium, <3 years = Low
- 🏷️ **Brand Reliability (30 points max)**: Enterprise > Consumer > Unknown brands
- 📂 **Device Category (20 points max)**: Critical > Business > Standard equipment
- 📊 **Total Risk Classification**: 70+ = HIGH, 35-69 = MEDIUM, <35 = LOW

## 📊 **Data Quality Pipeline**

### **Phase 1: Initial Validation**
```
Raw Inventory Data (3,928 devices)
    ↓
├── Brand Validation (Recognized vs Unrecognized)
├── Category Validation (Valid vs Invalid)
├── Purchase Date Validation (Valid vs Invalid)
└── Status Validation (Active vs Inactive)
```

### **Phase 2: Advanced Data Cleaning**
```
Invalid Data Identification
    ↓
├── Exclude Inactive Devices (handled separately)
├── Exclude Invalid Purchase Dates (handled separately)  
├── Attempt Data Recovery from Description/Model fields
└── Move Corrected Devices to Enhanced Dataset
```

### **Phase 3: Analysis-Ready Dataset**
```
Enhanced Fully Valid Data
    ↓
Filter to Active Devices Only
    ↓
Analysis Ready Data (Final dataset for risk analysis)
```

## 📋 **Excel Output Sheets**

### **Data Analyzer Output (`device_analysis_with_categories.xlsx`)**

| Sheet Name | Purpose | Color |
|------------|---------|-------|
| **Original_Data** | Unmodified source data | Blue |
| **Recognized_Brands** | Devices with valid brand names | Green |
| **Unrecognized_Brands** | Devices needing brand correction | Red |
| **Recognized_Categories** | Devices with valid categories | Green |
| **Unrecognized_Categories** | Devices needing category correction | Red |
| **Available_Active_Devices** | Devices available for use | Green |
| **Unavailable_Inactive_Devices** | Disposed/broken/donated devices | Red |
| **Valid_Purchase_Dates** | Devices with valid purchase dates | Green |
| **Invalid_Purchase_Dates** | Devices needing date correction | Red |
| **Fully_Valid_Data** | Original clean dataset | Green |
| **Enhanced_Fully_Valid_Data** | Improved dataset after corrections | Bright Green |
| **Analysis_Ready_Data** | Final dataset (enhanced + active only) | Gold |
| **All_Invalid_Data** | Comprehensive problem device list | Red |
| **Data_Quality_Summary** | Executive dashboard with metrics | Purple |

### **Risk Analyzer Output (`device_lifecycle_risk_analysis.xlsx`)**

| Sheet Name | Purpose | Color |
|------------|---------|-------|
| **Complete_Risk_Analysis** | Full risk analysis with scores | Dark Blue |
| **Risk_Summary_Dashboard** | Executive summary statistics | Purple |
| **Brand_Risk_Analysis** | Risk analysis by brand | Orange |
| **Category_Risk_Analysis** | Risk analysis by category | Teal |
| **Age_Distribution_Analysis** | Device age distribution insights | Deep Purple |
| **HIGH_RISK_Devices** | Immediate replacement needed (6 months) | Red |
| **MEDIUM_RISK_Devices** | Planned replacement (6-18 months) | Yellow |
| **LOW_RISK_Devices** | Good condition (18+ months) | Green |

## 🚀 **Usage Instructions**

### **Step 1: Data Cleaning & Validation**
```bash
python device_analyzer_with_categories.py
```
**What it does:**
- Reads `Inventory.csv`
- Performs comprehensive data validation
- Attempts advanced data recovery
- Creates `device_analysis_with_categories.xlsx`

**Expected Output:**
```
📊 Data Quality Results:
🎯 Enhanced Data Quality Score: 82.2% (3227/3928 devices)
📈 Improvement: +15 devices recovered through advanced cleaning
✅ Ready for DLM Risk Analysis: 3227 fully validated devices
```

### **Step 2: Risk Analysis & Lifecycle Planning**
```bash
python device_lifecycle_risk_analyzer.py
```
**What it does:**
- Reads `Analysis_Ready_Data` sheet from previous step
- Calculates comprehensive risk scores
- Categorizes devices by replacement priority
- Creates `device_lifecycle_risk_analysis.xlsx`

**Expected Output:**
```
📊 EXECUTIVE SUMMARY:
🔴 384 devices need IMMEDIATE attention (replacement within 6 months)
🟡 1360 devices need PLANNED replacement (6-18 months)
🟢 1802 devices are in good condition (18+ months)
```

## 💡 **Business Value**

### **For IT Managers:**
- 📈 **Strategic Planning**: Data-driven replacement schedules
- 💰 **Budget Optimization**: Prioritized spending on highest-risk devices
- 📊 **Executive Reporting**: Clear metrics and recommendations
- 🎯 **Risk Mitigation**: Proactive replacement before failures

### **For Data Quality:**
- 🧹 **Automated Cleaning**: Reduces manual data correction effort
- 📋 **Standardization**: Consistent brand and category naming
- 🔍 **Data Recovery**: Salvages information from incomplete records
- 📊 **Quality Metrics**: Clear visibility into data health

### **For Procurement:**
- 📅 **Replacement Timeline**: 6-month, 12-month, and 18-month planning horizons
- 🏷️ **Brand Analysis**: Performance insights by manufacturer
- 📂 **Category Priorities**: Equipment type risk assessments
- 💰 **Cost Planning**: Risk-based budget allocation

## 🔧 **Configuration & Customization**

### **Brand Recognition**
Modify brand lists in `device_analyzer_with_categories.py`:
```python
recognized_brands = ['HP', 'Dell', 'Apple', 'Lenovo', ...]  # Add new brands here
```

### **Category Classification**
Update category lists:
```python
recognized_categories = ['Desktop', 'Laptop', 'Tablet', ...]  # Add new categories
```

### **Risk Scoring**
Adjust risk thresholds in `device_lifecycle_risk_analyzer.py`:
```python
# Age-based risk scoring
if age_years >= 5:     # Modify age thresholds
    return 50, 'High Risk (5+ years old)'
```

### **Purchase Date Range**
Modify acceptable date range:
```python
min_year = 2010  # Adjust minimum acceptable year
max_year = 2025  # Adjust maximum acceptable year
```

## 📋 **Data Requirements**

### **Required CSV Columns:**
- `Asset Tag ID` - Unique device identifier
- `Brand` - Device manufacturer
- `Category` - Device type/category
- `Purchase Date` - Device purchase date
- `Status` - Device availability status
- `Description` - Device description (for data recovery)
- `Model` - Device model (for data recovery)

### **Supported Status Values:**
**Active/Available:** Available, Checked out, Check in, Under repair, Found, Reserved
**Inactive/Unavailable:** Broken, Disposed, Donated, Lost/Missing, Sold

## 🐛 **Troubleshooting**

### **Common Issues:**

**Error: "Could not find the CSV file"**
- Ensure `Inventory.csv` is in the same directory as the Python scripts
- Check file name spelling and case sensitivity

**Error: "Permission denied when trying to save"**
- Close any open Excel files before running
- Ensure you have write permissions to the output directory

**Error: "Analysis_Ready_Data sheet not found"**
- Run `device_analyzer_with_categories.py` first
- Ensure the analyzer completed successfully

**Low data quality scores:**
- Review brand and category recognition lists
- Check for unusual data formats in your inventory
- Consider manual data cleanup for critical missing information

## 📈 **Performance Metrics**

### **Typical Processing Times:**
- **Data Analysis**: ~30-60 seconds for 4,000 devices
- **Risk Analysis**: ~15-30 seconds for clean data
- **Excel Generation**: ~10-20 seconds with formatting

### **Expected Data Quality Improvements:**
- **Brand Recognition**: 85-95% with standard manufacturers
- **Category Classification**: 90-98% with common device types
- **Date Validation**: 95-99% with proper date formats
- **Overall Enhancement**: 5-15% improvement through data recovery

## 🔄 **Future Enhancements**

- 📊 **Dashboard Integration**: Web-based reporting interface
- 📱 **Mobile Access**: Device lookup and status updates
- 🔔 **Automated Alerts**: Proactive replacement notifications
- 📈 **Trend Analysis**: Historical risk progression tracking
- 🏷️ **Asset Tracking**: Integration with asset management systems

## 📞 **Support**

For questions, issues, or enhancement requests, please refer to the workflow diagram (`DLM_Workflow_Diagram.md`) for detailed process flow information.

---

**Last Updated:** July 23, 2025  
**Version:** 2.0 - Enhanced Data Cleaning & Status Validation
