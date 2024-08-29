# Replit Setup Guide Part 1: Vite + React + TypeScript + Tailwind CSS + shadcn/ui

## Version: 3.1
Last Updated: 2024-08-28

This guide covers the setup of the frontend environment for a Vite + React + TypeScript project with Tailwind CSS and shadcn/ui on Replit.

### 1. Create a New Vite Project

Create a new Vite project with React and TypeScript:

```bash
npm create vite@latest . -- --template react-ts
```

### 2. Install Dependencies

Install frontend dependencies:

```bash
npm install react react-dom @radix-ui/react-slot class-variance-authority clsx tailwind-merge
npm install -D @types/node @types/react @types/react-dom @vitejs/plugin-react typescript tailwindcss postcss autoprefixer vite tailwindcss-animate
```

### 3. Configure Tailwind CSS

Generate Tailwind config files:

```bash
npx tailwindcss init -p
```

Update `tailwind.config.js`:

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  darkMode: ["class"],
  content: [
    './pages/**/*.{ts,tsx}',
    './components/**/*.{ts,tsx}',
    './app/**/*.{ts,tsx}',
    './src/**/*.{ts,tsx}',
  ],
  theme: {
    container: {
      center: true,
      padding: "2rem",
      screens: {
        "2xl": "1400px",
      },
    },
    extend: {
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        secondary: {
          DEFAULT: "hsl(var(--secondary))",
          foreground: "hsl(var(--secondary-foreground))",
        },
        destructive: {
          DEFAULT: "hsl(var(--destructive))",
          foreground: "hsl(var(--destructive-foreground))",
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))",
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))",
        },
        popover: {
          DEFAULT: "hsl(var(--popover))",
          foreground: "hsl(var(--popover-foreground))",
        },
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))",
        },
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
      keyframes: {
        "accordion-down": {
          from: { height: 0 },
          to: { height: "var(--radix-accordion-content-height)" },
        },
        "accordion-up": {
          from: { height: "var(--radix-accordion-content-height)" },
          to: { height: 0 },
        },
      },
      animation: {
        "accordion-down": "accordion-down 0.2s ease-out",
        "accordion-up": "accordion-up 0.2s ease-out",
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
}
```

### 4. Set Up Global Styles

Create `src/globals.css`:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
    --card: 0 0% 100%;
    --card-foreground: 222.2 84% 4.9%;
    --popover: 0 0% 100%;
    --popover-foreground: 222.2 84% 4.9%;
    --primary: 222.2 47.4% 11.2%;
    --primary-foreground: 210 40% 98%;
    --secondary: 210 40% 96.1%;
    --secondary-foreground: 222.2 47.4% 11.2%;
    --muted: 210 40% 96.1%;
    --muted-foreground: 215.4 16.3% 46.9%;
    --accent: 210 40% 96.1%;
    --accent-foreground: 222.2 47.4% 11.2%;
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 210 40% 98%;
    --border: 214.3 31.8% 91.4%;
    --input: 214.3 31.8% 91.4%;
    --ring: 222.2 84% 4.9%;
    --radius: 0.5rem;
  }

  body {
    @apply bg-background text-foreground;
  }
}
```

### 5. Update Main Entry Point

Update `src/main.tsx`:

```typescript
import "./globals.css"
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.tsx'

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

### 6. Set Up Utility Functions

Create `src/lib/utils.ts`:

```typescript
import { type ClassValue, clsx } from "clsx"
import { twMerge } from "tailwind-merge"

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs))
}
```

### 7. Initialize shadcn/ui

Run the shadcn/ui initialization:

```bash
npx shadcn-ui@latest init
```

During the initialization process, you'll be prompted with several questions. Here are the recommended answers:

1. Would you like to use TypeScript (recommended)? › Yes
2. Which style would you like to use? › Default
3. Which color would you like to use as base color? › Slate
4. Where is your global CSS file? › src/globals.css
5. Do you want to use CSS variables for colors? › Yes
6. Where is your tailwind.config.js located? › tailwind.config.js
7. Configure the import alias for components: › @/components
8. Configure the import alias for utils: › @/lib/utils
9. Are you using React Server Components? › No
10. Write configuration to components.json. Proceed? › Yes

After the initialization is complete, add the Button component:

```bash
npx shadcn-ui@latest add button
```

This will add the Button component to your project, which you can then import and use in your React components.

### Update tsconfig.json for shadcn/ui

After initializing shadcn/ui, update your `tsconfig.json` to include the correct path aliases:

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "composite": true,
    "noEmit": true,
    "jsx": "react-jsx",
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```


Update 'tsconfig.node.json': 

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "lib": ["ES2023"],
    "module": "ESNext",
    "skipLibCheck": true,

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "isolatedModules": true,
    "moduleDetection": "force",
    "emit": true,
    "composite": true,

    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true
  },
  "include": ["vite.config.ts"]
}

```

### Update vite.config.ts for path aliasing

Update your `vite.config.ts`:

```typescript
import path from "path"
import react from "@vitejs/plugin-react"
import { defineConfig } from "vite"

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
})
```





With these steps completed, your frontend environment is set up and ready for development. Proceed to Part 2 for backend setup and final configurations.

# Replit Setup Guide Part 2: Express Backend + Final Configurations

## Version: 3.1
Last Updated: 2024-08-28

This guide covers the setup of the Express backend and final configurations for a Vite + React + TypeScript project with Tailwind CSS and shadcn/ui on Replit.

### 1. Install Backend Dependencies

Install the necessary backend dependencies:

```bash
npm install express cors
npm install -D @types/express @types/cors ts-node nodemon concurrently typescript @types/node tsconfig-paths
```

### 2. Create Express Server

Create a new file `server/index.ts`:

```
mkdir -p server
touch server/index.ts
```


```typescript
import express from 'express';
import cors from 'cors';
import path from 'path';
import { fileURLToPath } from 'url';

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

const app = express();
const PORT = process.env.PORT || 3000;

app.use(cors());
app.use(express.json());

// API routes
app.get('/api/hello', (_req, res) => {
  res.json({ message: 'Hello from the server!' });
});

// Determine the correct static file path
const staticPath = process.env.NODE_ENV === 'production'
  ? path.join(__dirname, '../dist')
  : path.join(__dirname, '..');

// Serve static files
app.use(express.static(staticPath));

// The "catch-all" handler
app.get('*', (_req, res) => {
  res.sendFile(path.join(staticPath, 'index.html'));
});

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

### 3. Configure TypeScript for Server

Create then update `tsconfig.server.json`:


```
touch tsconfig.server.json
```

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ESNext",
    "moduleResolution": "node",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "outDir": "./dist/server",
    "rootDir": "./server",
    "noEmit": false
  },
  "include": ["server/**/*"],
  "ts-node": {
    "esm": true,
    "experimentalSpecifierResolution": "node"
  }
}
```

### 4. Update Frontend App

Update `src/App.tsx` to include an API call and use the shadcn/ui Button:

```typescript
import { useState, useEffect } from 'react'
import { Button } from "@/components/ui/button"

function App() {
  const [message, setMessage] = useState('');

  useEffect(() => {
    fetch('/api/hello')
      .then(response => response.json())
      .then(data => setMessage(data.message));
  }, []);

  return (
    <div className="flex flex-col items-center justify-center h-screen bg-background text-foreground gap-4">
      <h1 className="text-4xl font-bold text-primary">
        Hello, Vite + React + Tailwind + shadcn/ui + Express on Replit!
      </h1>
      <Button>I'm a shadcn/ui button</Button>
      <p>{message}</p>
    </div>
  )
}

export default App
```

### 5. Configure Vite

Update `vite.config.ts`:

```typescript
import path from "path"
import react from "@vitejs/plugin-react"
import { defineConfig } from "vite"

export default defineConfig(({ command }) => {
  const commonConfig = {
    plugins: [react()],
    resolve: {
      alias: {
        "@": path.resolve(__dirname, "./src"),
      },
    },
  }

  if (command === 'serve') {
    return {
      ...commonConfig,
      server: {
        host: '0.0.0.0',
        port: 5173,
        strictPort: true,
        hmr: {
          clientPort: 443 // This is for Replit
        },
        proxy: {
          '/api': {
            target: 'http://localhost:3000',
            changeOrigin: true,
          },
        },
      },
    }
  } else {
    // Production build configuration
    return {
      ...commonConfig,
      build: {
        outDir: 'dist/client',
        emptyOutDir: true,
        rollupOptions: {
          output: {
            manualChunks: undefined,
          },
        },
      },
    }
  }
})
```

### 6. Update Package.json

Update `package.json`:

```json
  {
  "name": "vite-react-typescript-tailwind-shadcn-express",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev:all": "concurrently \"npm run dev\" \"ts-node-esm server/index.ts\"",
    "dev": "vite --host 0.0.0.0 --port 5173",
    "build": "npm run build:client && npm run build:server",
    "build:client": "tsc && vite build",
    "build:server": "tsc -p tsconfig.server.json",
    "lint": "eslint src --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview",
    "server": "node dist/server/index.js",
    "start": "node dist/server/index.js",
    "prod": "npm run build && npm run start"
  },
  "dependencies": {
    "@radix-ui/react-slot": "^1.1.0",
    "class-variance-authority": "^0.6.1",
    "clsx": "^1.2.1",
    "cors": "^2.8.5",
    "express": "^4.18.2",
    "http-proxy-middleware": "^3.0.0",
    "lucide-react": "^0.436.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "tailwind-merge": "^1.14.0"
  },
  "devDependencies": {
    "@types/cors": "^2.8.13",
    "@types/express": "^4.17.17",
    "@types/node": "^20.3.1",
    "@types/react": "^18.0.37",
    "@types/react-dom": "^18.0.11",
    "@typescript-eslint/eslint-plugin": "^5.59.0",
    "@typescript-eslint/parser": "^5.59.0",
    "@vitejs/plugin-react": "^4.0.0",
    "autoprefixer": "^10.4.14",
    "concurrently": "^8.2.0",
    "eslint": "^8.38.0",
    "eslint-plugin-react-hooks": "^4.6.0",
    "eslint-plugin-react-refresh": "^0.3.4",
    "nodemon": "^3.1.4",
    "postcss": "^8.4.24",
    "tailwindcss": "^3.3.2",
    "tailwindcss-animate": "^1.0.7",
    "ts-node": "^10.9.1",
    "tsconfig-paths": "^4.2.0",
    "typescript": "^5.0.2",
    "vite": "^4.3.9"
  }
}


```

### 7. Configure Replit

Create or update `.replit` file:

```
run = "npm run dev:all"
hidden = [".config", "tsconfig.json", "tsconfig.node.json", "vite.config.ts", ".gitignore"]

[env]
PATH = "/home/runner/$REPL_SLUG/.config/npm/node_global/bin:/home/runner/$REPL_SLUG/node_modules/.bin"

[nix]
channel = "stable-22_11"

[deployment]
build = ["sh", "-c", "npm install && npm run build"]
run = ["sh", "-c", "npm run prod"]
deploymentTarget = "cloudrun"

[[ports]]
localPort = 3000
externalPort = 3000

[[ports]]
localPort = 5173
externalPort = 80

```

Update `replit.nix`:

```nix
{ pkgs }: {
    deps = [
        pkgs.nodejs-18_x
        pkgs.nodePackages.typescript-language-server
        pkgs.yarn
        pkgs.replitPackages.jest
    ];
}
```

### 8. Start Development

To start both the frontend and backend servers, run:

```bash
npm run dev:all
```

This command will concurrently run the Vite development server for the frontend and the Express server for the backend.

### 9. Access Your Application

After starting the development servers:

1. The frontend will be accessible on port 5173 (mapped to 80 externally in Replit).
2. The backend API will be available on port 3001, proxied through the frontend server.

You can now access your full-stack application directly through the Replit interface or via the provided URL.

### 10. Further Development

With this setup, you can now:

- Add more React components in the `src` directory.
- Create new API endpoints in the `server/index.ts` file.
- Install and use additional shadcn/ui components as needed.
- Customize styles using Tailwind CSS classes.

Remember to commit your changes regularly if you're using version control.

Congratulations! Your Vite + React + TypeScript + Tailwind CSS + shadcn/ui + Express project is now fully set up and ready for development on Replit.
Last edited just now
