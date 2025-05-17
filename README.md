# 🎨 Matplotlib Customization in WSL2 🚀  

## Overview  
While learning **Matplotlib** through [this tutorial video](https://youtu.be/3Xc3CA655Y4?si=gTZJfWlxZPo44Q5C), I explored various **graphing techniques, color customizations, and data visualization methods**. Along the way, I encountered an issue where **Comic Sans MS wouldn't load** properly, prompting me to troubleshoot and find a fix.  

This project documents both my learning experience and the steps I took to resolve the font issue within **WSL2 (Ubuntu 24 LTS)**.

## 📚 Learning Highlights  
Through this tutorial, I learned how to:  
- 📊 **Create Basic Graphs** (Line Graphs, Histograms, Pie Charts, Box-and-Whisker Plots)  
- 🎨 **Style Plots with Custom Colors, Line Types, Titles, and Labels**  
- 🛠️ **Fine-tune Axis Ticks, Legends, and Layouts for Better Visualization**  
- 🚀 **Integrate Matplotlib with WSL2 for seamless execution in Ubuntu**  

## 🔍 Fixing the Comic Sans MS Issue  
During my exploration, I noticed Matplotlib **couldn’t recognize Comic Sans MS**, despite its availability on Windows. I followed these steps to resolve the issue:  

### 1️⃣ Check Font Availability  
```bash
fc-list | grep "Comic Sans MS"
```
Confirmed that **Comic Sans MS** was available but wasn’t detected by Matplotlib.  

### 2️⃣ Configure Fontconfig to Use Windows Fonts  
```bash
sudo nano /etc/fonts/local.conf
```
Added:
```xml
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
    <dir>/mnt/c/Windows/Fonts</dir>
</fontconfig>
```
This ensured WSL2 could access Windows-installed fonts.  

### 3️⃣ Refresh Font Cache  
```bash
fc-cache -fv
```
Forced Matplotlib to re-scan the fonts.  

### 4️⃣ Verify Matplotlib’s Font Recognition  
```python
import matplotlib.font_manager as fm
font_paths = fm.findSystemFonts(fontpaths=["/mnt/c/Windows/Fonts"], fontext='ttf')
font_names = [fm.FontProperties(fname=fp).get_name() for fp in font_paths]
print(font_names)
```
Confirmed that **Comic Sans MS appeared in the list**, proving that Matplotlib could detect it.  

### 5️⃣ Clear Matplotlib’s Cached Font Data  
```bash
rm -rf ~/.cache/matplotlib
```
Removed outdated font cache, allowing Matplotlib to refresh its font list.  

## 📊 Example Plot Using Comic Sans MS  
After implementing the fix, Matplotlib successfully loaded **Comic Sans MS**, as shown below:  
```python
import matplotlib.pyplot as plt
import matplotlib
matplotlib.rcParams['font.family'] = 'Comic Sans MS'

x, y = [1, 2, 3], [2, 4, 6]
plt.plot(x, y)
plt.title('Matplotlib Font Fix!', fontsize=20)
plt.xlabel('X Axis')
plt.ylabel('Y Axis')
plt.show()
```

## 📂 Data Sources  
As part of my learning, I used the following datasets from the tutorial:  
- 🔗 **Gas Prices Dataset**: [GitHub Source](https://github.com/KeithGalli/matplotlib_tutorial/blob/master/gas_prices.csv)  
- 🔗 **FIFA Stats Dataset**: [GitHub Source](https://github.com/KeithGalli/matplotlib_tutorial/blob/master/fifa_data.csv)  

## 📜 Source Code & References  
- 📺 **Matplotlib Tutorial Video**: [YouTube](https://youtu.be/3Xc3CA655Y4?si=gTZJfWlxZPo44Q5C)  
- 📁 **Original Repository**: [GitHub](https://github.com/KeithGalli/matplotlib_tutorial/tree/master)  

## 💡 Summary & Takeaways  
Throughout this learning journey, I **built various types of graphs**, experimented with **custom styling**, and **fixed the Comic Sans MS issue in Matplotlib**. The main challenge was **Matplotlib's outdated font cache**, which prevented proper font recognition. **Clearing the cache and configuring Fontconfig** ultimately solved the issue, allowing me to fully control Matplotlib's styling within WSL2!  

---
🔍 **Want to Improve This Further?**  
Explore [Matplotlib’s documentation](https://matplotlib.org/stable/) for advanced techniques!