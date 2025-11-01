# Anaconda and VS Code Installation - Notes

## Anaconda Installation Guide

1. **Download Process**
   - Visit official Anaconda website
   - Choose appropriate version:
     - Windows/Mac/Linux
     - Python version compatibility
   - Download installer

2. **Installation Steps**
   - Run installer
   - Choose installation type:
     - Just Me (recommended)
     - All Users (requires admin)
   - Select installation path
   - Configure environment variables

3. **Verification**
   - Open Anaconda Navigator
   - Check conda version in terminal
   - Verify Python installation
   - Test package management

## VS Code Setup

1. **Initial Installation**
   - Download VS Code
   - Run installer
   - Add to PATH (Windows)
   - Enable file associations

2. **Essential Extensions**
   - Python extension
   - Jupyter extension
   - IntelliSense
   - Code formatting tools

3. **Configuration**
   - Python interpreter selection
   - Jupyter settings
   - Code formatting rules
   - Workspace settings

## Environment Configuration

1. **Conda Environment Management**
   ```bash
   # Create new environment
   conda create -n rag-bootcamp python=3.9
   
   # Activate environment
   conda activate rag-bootcamp
   
   # Install packages
   conda install jupyter pandas numpy
   ```

2. **VS Code Integration**
   - Select conda environment
   - Configure Python path
   - Set up debugging
   - Configure linting

## Troubleshooting Guide

1. **Common Anaconda Issues**
   - PATH variables
   - Environment activation
   - Package conflicts
   - Permission issues

2. **VS Code Problems**
   - Extension loading
   - Interpreter selection
   - Jupyter connection
   - IntelliSense issues