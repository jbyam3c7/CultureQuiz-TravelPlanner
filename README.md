# Cultural Match Assessment - README

## 🌍 Overview

The Cultural Match Assessment is a web-based personality quiz that helps people discover which world cultures align best with their values, lifestyle preferences, and personality traits. This tool recognizes that some people may resonate more deeply with cultures different from where they were born.

## 🎯 What This App Does

- **Analyzes** your personal preferences across 15 different cultural dimensions
- **Matches** you with countries/cultures that share your values and lifestyle
- **Shows** your top 3 cultural matches with compatibility percentages
- **Explains** why each culture matches based on specific traits

## 🚀 Getting Started (Complete Beginner's Guide)

### Option 1: Easiest Method - Direct Browser Opening

1. **Save the HTML file:**
   - Copy all the code from the HTML artifact
   - Open a text editor on your computer:
     - **Windows**: Notepad (search for "Notepad" in Start menu)
     - **Mac**: TextEdit (search for "TextEdit" in Spotlight)
     - **Linux**: gedit or any text editor
   
2. **Create the file:**
   - Paste the code into the text editor
   - Save the file with the name: `cultural-match-assessment.html`
   - **Important**: Make sure the file ends with `.html` not `.txt`
   
3. **Open in browser:**
   - Find the saved file on your computer
   - Double-click the file - it should open in your default web browser
   - If double-clicking doesn't work, right-click and select "Open with" → Choose your browser (Chrome, Firefox, Safari, Edge)

### Option 2: Using Visual Studio Code (Recommended for Editing)

1. **Install VS Code** (if you don't have it):
   - Go to https://code.visualstudio.com/
   - Download for your operating system
   - Install following the default options

2. **Create your project:**
   - Open VS Code
   - Click "File" → "New File"
   - Copy and paste the HTML code
   - Save it as `cultural-match-assessment.html`

3. **Install Live Server extension** (for better development experience):
   - Click the Extensions icon in VS Code (looks like 4 squares)
   - Search for "Live Server"
   - Click "Install" on the one by Ritwick Dey

4. **Run the app:**
   - Right-click on your HTML file in VS Code
   - Select "Open with Live Server"
   - Your browser will open automatically with the app running

### Option 3: Hosting Online (Share with Others)

#### Using GitHub Pages (Free):

1. **Create a GitHub account:**
   - Go to https://github.com
   - Sign up for a free account

2. **Create a new repository:**
   - Click the "+" icon in top right → "New repository"
   - Name it: `cultural-match-assessment`
   - Make it Public
   - Click "Create repository"

3. **Upload your file:**
   - Click "uploading an existing file"
   - Drag your `cultural-match-assessment.html` file into the browser
   - Rename it to `index.html` before uploading
   - Click "Commit changes"

4. **Enable GitHub Pages:**
   - Go to Settings (in your repository)
   - Scroll down to "Pages" in the left sidebar
   - Under "Source", select "Deploy from a branch"
   - Choose "main" branch and "/ (root)" folder
   - Click Save
   - Wait 5 minutes, then visit: `https://[your-username].github.io/cultural-match-assessment`

#### Using Netlify (Even Easier):

1. **Go to Netlify Drop:**
   - Visit https://app.netlify.com/drop

2. **Prepare your file:**
   - Make sure your HTML file is named `index.html`
   - Put it in a folder on its own

3. **Deploy:**
   - Drag the folder containing your `index.html` onto the Netlify Drop page
   - Your site will be instantly live with a random URL
   - You can claim the site to customize the URL (requires free account)

## 📱 System Requirements

### Minimum Requirements:
- Any modern web browser (2018 or newer):
  - Chrome 70+
  - Firefox 65+
  - Safari 12+
  - Edge 79+
- Works on all devices: Desktop, Tablet, Phone
- No internet connection required (once downloaded)
- No server or database needed

## 🎮 How to Use the App

1. **Start the Assessment:**
   - Open the app in your browser
   - Click "Begin Your Journey" button

2. **Answer Questions:**
   - Read each question carefully
   - For multiple choice: Click your preferred answer
   - For sliders: Drag to select your position between extremes
   - Use "Previous" button if you want to change an answer
   - Click "Next" to continue

3. **View Results:**
   - After 15 questions, click "See Results"
   - Review your top 3 cultural matches
   - Each match shows:
     - Country name and flag
     - Compatibility percentage
     - Key cultural traits that align with your answers

4. **Retake:**
   - Click "Take Again" to restart with different answers

## 🛠️ Customization Guide

### Changing Colors:

Find this section in the code:
```css
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
```
Replace `#667eea` and `#764ba2` with your preferred colors.
- Use color pickers: https://colorhunt.co/ or https://coolors.co/

### Adding More Countries:

1. Find the `cultures` array in the JavaScript section
2. Add a new country object following this template:
```javascript
{
    name: "Country Name",
    emoji: "🏴", // Find flag emojis at emojipedia.org
    score: 0,
    color: "#hexcolor",
    traits: ["Trait 1", "Trait 2", "Trait 3"],
    matches: {
        "answer-value": 3, // 3 = strong match, 2 = moderate, 1 = weak
    },
    sliderPreferences: { 1: 5, 6: 7 } // Question index: ideal value
}
```

### Modifying Questions:

Find the `questions` array and add/edit questions:
```javascript
{
    question: "Your question text?",
    type: "multiple", // or "slider"
    options: [
        { text: "Answer option", value: "answer-value" }
    ]
}
```

## 🐛 Troubleshooting

### Problem: File opens showing code instead of the app
**Solution**: Make sure the file is saved with `.html` extension, not `.txt`

### Problem: Buttons or sliders not working
**Solution**: 
- Try a different browser
- Make sure JavaScript is enabled in your browser settings
- Check that you copied ALL the code (from `<!DOCTYPE html>` to `</html>`)

### Problem: Layout looks broken
**Solution**: 
- Use a modern browser (update if needed)
- Try refreshing the page (Ctrl+F5 or Cmd+Shift+R)
- Check zoom level is at 100%

### Problem: Can't save the file as HTML
**Solution for Mac TextEdit**:
- Go to TextEdit → Preferences
- Under "Format", select "Plain text"
- Uncheck "Add .txt extension to plain text files"

**Solution for Windows**:
- When saving in Notepad, change "Save as type" to "All Files (*.*)"
- Type the full name including extension: `cultural-match-assessment.html`

## 📊 Understanding the Algorithm

The app calculates cultural matches based on:

1. **Multiple Choice Answers** (weighted 1-3 points):
   - Strong alignment = 3 points
   - Moderate alignment = 2 points  
   - Weak alignment = 1 point

2. **Slider Values** (0-10 points):
   - Calculates difference from culture's ideal value
   - Closer to ideal = more points

3. **Final Score**:
   - Combines all points
   - Converts to percentage relative to highest scoring culture
   - Displays top 3 matches

## 🤝 Sharing & Contributing

### Sharing Your Results:
- Take a screenshot of your results
- Share the app link if hosted online
- Download and email the HTML file to friends

### Improving the App:
- Add more nuanced questions
- Include more countries/regions
- Add subcultural options (urban vs rural)
- Create detailed explanations for each match
- Add a data export feature for results

## 📚 Learning Resources

If you want to understand or modify the code:

- **HTML Basics**: https://www.w3schools.com/html/
- **CSS Styling**: https://www.w3schools.com/css/
- **JavaScript**: https://javascript.info/
- **Free Code Editor**: https://code.visualstudio.com/

## 🆘 Getting Help

If you're stuck:
1. Re-read the relevant section of this README
2. Try the troubleshooting section
3. Search for your error message on Google
4. Ask for help on:
   - https://stackoverflow.com (for coding questions)
   - https://www.reddit.com/r/learnprogramming/

## 📄 License

This project is free to use, modify, and share. No attribution required, but appreciated!

## ✨ Credits

Created as an educational project to explore cultural compatibility and help people find where they might thrive in the world.

---

**Remember**: This assessment is for fun and self-discovery. Real cultures are complex and diverse - these are general patterns, not rules. Every country has people with all types of personalities!
