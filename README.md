# CSS3 Transitions, Animations, and Advanced JavaScript Functions

## Objectives

Create smooth CSS transitions and animations.
Use JavaScript functions for dynamic behavior.
Implement local storage for data persistence.

## Instructions
Add CSS animations to elements like buttons or images.

>[!NOTE]
> - Write a JavaScript function that:
> - Stores and retrieves user preferences using localStorage.
> - Implements an animation triggered by user actions.

## Tasks

Create a CSS animation.
Store data in localStorage.
Apply JavaScript to trigger animations.

Happy Coding! 💻✨

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Theme Preferences</title>
    <style>
        :root {
            --primary-color: #4a90e2;
            --secondary-color: #f39c12;
            --background-color: #f5f5f5;
            --text-color: #333;
            --transition-speed: 0.5s;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--background-color);
            color: var(--text-color);
            transition: background-color var(--transition-speed), 
                        color var(--transition-speed);
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            text-align: center;
            margin-bottom: 40px;
        }

        h1 {
            margin-bottom: 10px;
        }

        .theme-options {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 40px;
        }

        .theme-card {
            background-color: white;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            position: relative;
            overflow: hidden;
        }

        .theme-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        .theme-card.selected {
            border: 3px solid var(--primary-color);
        }

        .theme-card.selected::after {
            content: "✓";
            position: absolute;
            top: 10px;
            right: 10px;
            background-color: var(--primary-color);
            color: white;
            width: 24px;
            height: 24px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        .color-preview {
            height: 50px;
            border-radius: 4px;
            margin-bottom: 10px;
        }

        .custom-section {
            background-color: white;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            margin-bottom: 40px;
        }

        .form-group {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
        }

        input[type="color"] {
            width: 100%;
            height: 40px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        .button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 4px;
            padding: 12px 24px;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.2s;
            display: inline-block;
        }

        .button:hover {
            background-color: var(--secondary-color);
            transform: scale(1.05);
        }

        /* Button click animation */
        .button:active {
            transform: scale(0.95);
        }

        /* Toast Notification */
        .toast {
            position: fixed;
            bottom: -100px;
            left: 50%;
            transform: translateX(-50%);
            background-color: #333;
            color: white;
            padding: 15px 30px;
            border-radius: 4px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.2);
            transition: bottom 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            z-index: 1000;
        }

        .toast.show {
            bottom: 30px;
        }

        /* Animation for new elements */
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .animated {
            animation: fadeIn 0.6s ease-out forwards;
        }

        /* Dark Mode Styles */
        body.dark-mode {
            --background-color: #222;
            --text-color: #f5f5f5;
        }

        body.dark-mode .theme-card,
        body.dark-mode .custom-section {
            background-color: #333;
            color: #f5f5f5;
        }

        /* Toggle Switch */
        .toggle-switch {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 20px;
        }

        .switch {
            position: relative;
            display: inline-block;
            width: 60px;
            height: 34px;
            margin: 0 10px;
        }

        .switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }

        .slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #ccc;
            transition: .4s;
            border-radius: 34px;
        }

        .slider:before {
            position: absolute;
            content: "";
            height: 26px;
            width: 26px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            transition: .4s;
            border-radius: 50%;
        }

        input:checked + .slider {
            background-color: var(--primary-color);
        }

        input:checked + .slider:before {
            transform: translateX(26px);
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Theme Preferences</h1>
            <p>Customize your experience and save your preferences</p>
        </header>

        <div class="toggle-switch">
            <span>Light Mode</span>
            <label class="switch">
                <input type="checkbox" id="dark-mode-toggle">
                <span class="slider"></span>
            </label>
            <span>Dark Mode</span>
        </div>

        <h2>Choose a Theme</h2>
        <div class="theme-options">
            <div class="theme-card" data-theme="blue">
                <div class="color-preview" style="background-color: #4a90e2;"></div>
                <h3>Blue Theme</h3>
                <p>Classic blue with modern accents</p>
            </div>
            
            <div class="theme-card" data-theme="green">
                <div class="color-preview" style="background-color: #2ecc71;"></div>
                <h3>Green Theme</h3>
                <p>Fresh and natural look</p>
            </div>
            
            <div class="theme-card" data-theme="purple">
                <div class="color-preview" style="background-color: #9b59b6;"></div>
                <h3>Purple Theme</h3>
                <p>Rich and elegant design</p>
            </div>
            
            <div class="theme-card" data-theme="orange">
                <div class="color-preview" style="background-color: #e67e22;"></div>
                <h3>Orange Theme</h3>
                <p>Warm and inviting colors</p>
            </div>
        </div>

        <div class="custom-section">
            <h2>Customize Your Theme</h2>
            <div class="form-group">
                <label for="primary-color">Primary Color</label>
                <input type="color" id="primary-color" value="#4a90e2">
            </div>
            
            <div class="form-group">
                <label for="secondary-color">Secondary Color</label>
                <input type="color" id="secondary-color" value="#f39c12">
            </div>
            
            <button id="apply-button" class="button">Apply Custom Theme</button>
            <button id="reset-button" class="button" style="margin-left: 10px; background-color: #e74c3c;">Reset</button>
        </div>

        <div class="preview-section custom-section">
            <h2>Preview</h2>
            <p>This is how your selected theme will look across the site</p>
            
            <div style="margin-top: 20px;">
                <button id="demo-button" class="button">Sample Button</button>
                <p style="margin-top: 20px;">Text with <a href="#" style="color: var(--primary-color);">colored links</a> and content.</p>
            </div>
        </div>
    </div>

    <div id="toast" class="toast">Preferences saved successfully!</div>

    <script>
        // DOM Elements
        const themeCards = document.querySelectorAll('.theme-card');
        const primaryColorInput = document.getElementById('primary-color');
        const secondaryColorInput = document.getElementById('secondary-color');
        const applyButton = document.getElementById('apply-button');
        const resetButton = document.getElementById('reset-button');
        const demoButton = document.getElementById('demo-button');
        const toast = document.getElementById('toast');
        const darkModeToggle = document.getElementById('dark-mode-toggle');

        // Default themes
        const themes = {
            blue: {
                primary: '#4a90e2',
                secondary: '#f39c12'
            },
            green: {
                primary: '#2ecc71',
                secondary: '#e74c3c'
            },
            purple: {
                primary: '#9b59b6',
                secondary: '#3498db'
            },
            orange: {
                primary: '#e67e22',
                secondary: '#2980b9'
            }
        };

        // Load saved preferences from localStorage
        function loadPreferences() {
            const savedPreferences = getUserPreferences();
            
            if (savedPreferences) {
                // Set the colors from saved preferences
                document.documentElement.style.setProperty('--primary-color', savedPreferences.primaryColor);
                document.documentElement.style.setProperty('--secondary-color', savedPreferences.secondaryColor);
                
                // Update color inputs
                primaryColorInput.value = savedPreferences.primaryColor;
                secondaryColorInput.value = savedPreferences.secondaryColor;
                
                // Select the correct theme card if applicable
                themeCards.forEach(card => {
                    card.classList.remove('selected');
                    if (card.dataset.theme === savedPreferences.theme) {
                        card.classList.add('selected');
                    }
                });

                // Set dark mode if saved
                if (savedPreferences.darkMode) {
                    document.body.classList.add('dark-mode');
                    darkModeToggle.checked = true;
                } else {
                    document.body.classList.remove('dark-mode');
                    darkModeToggle.checked = false;
                }
            }
        }

        // Save user preferences to localStorage
        function saveUserPreferences(preferences) {
            localStorage.setItem('userThemePreferences', JSON.stringify(preferences));
            showToast();
        }

        // Get user preferences from localStorage
        function getUserPreferences() {
            const preferences = localStorage.getItem('userThemePreferences');
            return preferences ? JSON.parse(preferences) : null;
        }

        // Apply theme based on selection
        function applyTheme(themeName) {
            const theme = themes[themeName];
            if (theme) {
                document.documentElement.style.setProperty('--primary-color', theme.primary);
                document.documentElement.style.setProperty('--secondary-color', theme.secondary);
                
                // Update color inputs
                primaryColorInput.value = theme.primary;
                secondaryColorInput.value = theme.secondary;
                
                // Save preferences
                saveUserPreferences({
                    theme: themeName,
                    primaryColor: theme.primary,
                    secondaryColor: theme.secondary,
                    darkMode: darkModeToggle.checked
                });
            }
        }

        // Apply custom theme
        function applyCustomTheme() {
            const primaryColor = primaryColorInput.value;
            const secondaryColor = secondaryColorInput.value;
            
            document.documentElement.style.setProperty('--primary-color', primaryColor);
            document.documentElement.style.setProperty('--secondary-color', secondaryColor);
            
            // Remove selection from all theme cards
            themeCards.forEach(card => {
                card.classList.remove('selected');
            });
            
            // Save custom theme preferences
            saveUserPreferences({
                theme: 'custom',
                primaryColor: primaryColor,
                secondaryColor: secondaryColor,
                darkMode: darkModeToggle.checked
            });
            
            // Animate the apply button
            animateElement(applyButton);
        }

        // Reset to default theme
        function resetTheme() {
            document.documentElement.style.setProperty('--primary-color', '#4a90e2');
            document.documentElement.style.setProperty('--secondary-color', '#f39c12');
            document.body.classList.remove('dark-mode');
            darkModeToggle.checked = false;
            
            // Update color inputs
            primaryColorInput.value = '#4a90e2';
            secondaryColorInput.value = '#f39c12';
            
            // Remove selection from all theme cards
            themeCards.forEach(card => {
                card.classList.remove('selected');
            });
            
            // Reset saved preferences
            localStorage.removeItem('userThemePreferences');
            
            // Animate the reset button
            animateElement(resetButton);
            showToast('Preferences reset to default');
        }

        // Show toast notification
        function showToast(message = 'Preferences saved successfully!') {
            toast.textContent = message;
            toast.classList.add('show');
            
            setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }

        // Animation function for elements
        function animateElement(element) {
            // Remove animation class if it exists
            element.classList.remove('animated');
            
            // Trigger reflow to restart animation
            void element.offsetWidth;
            
            // Add animation class
            element.classList.add('animated');
        }

        // Demo button animation
        function demoButtonAnimation() {
            demoButton.style.backgroundColor = 'var(--secondary-color)';
            
            setTimeout(() => {
                demoButton.style.backgroundColor = 'var(--primary-color)';
            }, 500);
            
            animateElement(demoButton);
        }

        // Toggle dark mode
        function toggleDarkMode() {
            document.body.classList.toggle('dark-mode');
            
            // Save the current preferences with updated dark mode setting
            const currentPreferences = getUserPreferences() || {
                theme: 'blue',
                primaryColor: primaryColorInput.value,
                secondaryColor: secondaryColorInput.value
            };
            
            currentPreferences.darkMode = darkModeToggle.checked;
            saveUserPreferences(currentPreferences);
        }

        // Event Listeners
        themeCards.forEach(card => {
            card.addEventListener('click', () => {
                const themeName = card.dataset.theme;
                
                // Remove selection from all cards
                themeCards.forEach(c => c.classList.remove('selected'));
                
                // Select the clicked card
                card.classList.add('selected');
                
                // Apply the selected theme
                applyTheme(themeName);
                
                // Animate the card
                animateElement(card);
            });
        });

        applyButton.addEventListener('click', applyCustomTheme);
        resetButton.addEventListener('click', resetTheme);
        demoButton.addEventListener('click', demoButtonAnimation);
        darkModeToggle.addEventListener('change', toggleDarkMode);

        // Initialize with saved preferences
        document.addEventListener('DOMContentLoaded', loadPreferences);
    </script>
</body>
</html>
