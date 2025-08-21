const express = require('express');
const puppeteer = require('puppeteer');
const app = express();

app.get('/generate-prompt', async (req, res) => {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  // 访问部署在 GitHub Pages 等的组件页面
  await page.goto('https://your-github-component-page.com'); 
  // 假设组件有生成提示词的按钮，模拟点击
  await page.click('#generate-btn'); 
  // 提取生成的提示词内容（根据组件实际 DOM 结构）
  const prompt = await page.$eval('.prompt-content', el => el.textContent); 
  await browser.close();
  res.send({ prompt });
});

app.listen(3000, () => console.log('服务启动'));
