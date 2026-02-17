name: Next JS Build with Caching & Artifacts

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Setup Node JS
        uses: actions/setup-node@v4.2.2
        with:
          node-version: 22.x
          cache: 'npm'

      - name: Install Dependencies
        run: npm install

      - name: Build Next JS App
        run: npm run build

      - name: Upload Build Artifacts
        uses: actions/upload-artifact@v4.6.0
        with:
          name: nextjs-build
          path: out/
