# Terminal Portfolio with Svelte

A modern Linux-style interactive portfolio built with Svelte, Javascript, and CSS.

## Screenshot

![Home](/public/home.png)
![Contact](/public/contact.png)
![Neofetch](/public/neofetch.png)
![Projects](/public/project.png)

## ✨ Features

- 🔧 Fully interactive terminal experience
- 📁 Display homescreen with ascii art
- 🎨 Neofetch
- 📱 List of social media
- ⚡ Show information about developer and projects
- 🔄 Run calculator

## 🚀 Available Commands

| Command      | Description                  |
| ------------ | ---------------------------- |
| `about`      | Display about me information |
| `contact`    | Show contact information     |
| `calc 7 + 3` | Run calculator               |
| `home`       | Show homescreen              |
| `neofetch`   | Show a specification         |
| `projects`   | List of projects             |
| `clear`      | Clear terminal               |
| `help`       | Show available commands      |
|              |                              |

## 🛠️ Tech Stack

- [Svelte](https://svelte.dev/) - Frontend framework
- [Vite](https://vitejs.dev/) - Build tool  

## 📦 Installation

1. Clone repository:
   ```bash
   git clone https://github.com/zulhaditya/porterminal.git
   cd porterminal
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Run development server:
   ```bash
   npm run dev
   ```

4. Build for production:
   ```bash
   npm run build
   ```

## 🌈 Customization

### Add New Commands
1. Create new file in `src/commands/`:
   ```html
   <!-- MyCommand.svelte -->
   <script lang="ts">
     export let args: string[] = [];
   </script>

   <div class="command-output">
     Your command output here
   </div>
   ```

2. Register command in `Terminal.svelte`:
   ```javascript
   const commands = {
     // ...
     mycmd: MyCommand
   };
   ```

### Change Theme
Edit `src/app.css`:
```css
:root {
  --primary: #4af626; /* Terminal green */
  --bg: #1e1e1e;     /* Background color */
}
```

## 🧪 Testing
Run test suite:
```bash
npm test
```

## 🤝 Contributing
1. Fork the project  
2. Create feature branch (`git checkout -b feature/latest-feature`)
3. Commit changes (`git commit -m 'Add latest feature'`)
4. Push to branch (`git push origin feature/latest-feature`)  
5. Open Pull Request
