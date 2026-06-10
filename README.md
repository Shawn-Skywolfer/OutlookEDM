# Outlook EDM 制作专家 / Outlook EDM Maker

[中文说明](#中文说明) · [English Guide](#english-guide)

---

# 中文说明

## 项目简介

Outlook EDM 制作专家是一款运行在浏览器中的 EDM 邮件制作工具。它支持直接组合多张图片，也支持将一张完整长图切割成多个切片，最后生成可由 Microsoft Outlook 打开的 `.eml` 邮件文件。

项目采用单文件前端实现，无需安装或构建。上传图片的读取、切片、预览和邮件生成均在当前浏览器本地完成，项目不会主动将图片上传到服务器。

## 主要功能

- **中英双语界面 / Bilingual interface**
  - 点击页面右上角的 `中文 / EN` 可随时切换界面语言。
  - Use the `中文 / EN` control in the upper-right corner to switch languages at any time.
  - 语言偏好会保存在浏览器中，并在下次打开时自动恢复。
  - Your language preference is saved in the browser and restored on your next visit.

- **上传切片模式**
  - 一次上传多张图片。
  - 根据文件名中的数字自动进行初始排序。
  - 在预览区拖拽图片以调整最终顺序。
  - 使用厘米设置 EDM 在邮件中的显示宽度。
  - 超出预览区域宽度时，可通过横向滚动条查看完整内容。

- **长图切割模式**
  - 上传一张完整设计长图。
  - 像 Photoshop 切片工具一样纵向拖拽创建横贯图片宽度的切片。
  - 支持切片边缘吸附、相邻切片边界联动调整和尺寸提示。
  - 支持删除切片、撤销和重做。
  - 将切割结果转换为可继续排序、预览和导出的图片切片。

- **EML 邮件生成**
  - 设置邮件主题。
  - 将图片作为 CID 内嵌资源写入邮件。
  - 生成可由 Outlook 打开的 `.eml` 文件。

## 运行要求

建议使用较新版本的桌面浏览器：

- Microsoft Edge
- Google Chrome

页面启动时需要联网加载：

- Tailwind CSS
- React 18
- React DOM 18
- Babel Standalone

> 图片处理在本地完成，但首次加载页面时必须能够访问 `index.html` 中配置的 CDN。

## 启动项目

### 直接打开

双击 `index.html`，或将其拖入浏览器窗口。

如果浏览器限制本地文件脚本，请使用本地 HTTP 服务器。

### 使用 Python（推荐）

在项目根目录运行：

```bash
python3 -m http.server 8080
```

访问：

```text
http://localhost:8080
```

### 使用 Node.js

```bash
npx serve .
```

按照终端显示的地址访问页面。

## 切换界面语言

页面默认显示中文。点击右上角的 **English** 按钮可切换为英文；在英文界面点击 **中文** 可切回中文。

- 语言选择会保存在当前浏览器的本地存储中。
- 下次打开页面时会继续使用上次选择的语言。
- 如果邮件主题仍为系统默认值，切换语言时默认主题也会同步翻译。
- 用户自行输入的邮件主题不会因语言切换而被覆盖。

## 使用方法一：直接上传已切好的图片

适合已经拥有多张连续 EDM 图片切片的情况。

### 1. 进入上传切片模式

点击顶部的 **上传切片模式**。

### 2. 设置邮件主题

在左侧 **邮件主题** 输入框中填写标题。该标题会用于邮件主题和下载的 `.eml` 文件名。

### 3. 设置图片显示宽度

在 **尺寸设置** 中输入图片显示宽度，单位为厘米。默认值为 `15 cm`。

该设置只控制最终邮件中的显示尺寸，不会修改原始文件；图片高度会按照原始宽高比自动计算。

### 4. 上传图片

点击 **上传多张切片文件**，一次选择一张或多张图片。

推荐使用连续编号：

```text
slice_01.jpg
slice_02.jpg
slice_03.jpg
```

工具会提取文件名中的第一个数字进行初始排序。未包含数字的文件会排在包含数字的文件之后。

### 5. 调整顺序并检查预览

在右侧 Outlook 预览中按住图片并拖到目标位置。预览顺序就是最终邮件顺序。

当目标宽度超过预览区域时，使用预览区底部的横向滚动条查看完整内容。

### 6. 生成 EML

确认主题、宽度和顺序后，点击右上角 **生成 EML 邮件**。浏览器会下载以邮件主题命名的 `.eml` 文件。

## 使用方法二：上传长图并切割

适合只有一张完整设计长图的情况。

### 1. 进入长图切割模式

点击顶部的 **长图切割模式**。

### 2. 上传长图

点击左侧 **上传一张设计长图** 并选择图片。该模式一次处理一张长图，重新上传会替换当前图片。

### 3. 创建切片

选择 **切片工具**，在尚未被切片占用的纵向区域：

1. 按住鼠标左键；
2. 向上或向下拖动；
3. 松开鼠标完成切片。

绘制时：

- 切片始终横贯图片完整宽度；
- 参考线显示当前纵向位置；
- 浮层显示切片的原始像素宽高；
- 靠近图片或已有切片边界时自动吸附；
- 切片不能越过相邻边界，也不能与已有切片重叠；
- 可以从图片左右两侧的灰色区域开始拖拽。

如果起点位于已有切片内部，本次绘制不会创建新切片。

### 4. 调整切片边界

在 **切片工具** 下，将鼠标移到切片上边缘或下边缘。命中时参考线会高亮，光标会变为纵向调整光标。

- 拖动公共边界会同时调整相邻的上下两个切片；
- 独立边缘不会越过相邻切片；
- 工具会保留最小切片高度；
- 边界继续应用吸附规则；
- 鼠标移出编辑区域后仍可继续当前拖动。

### 5. 选择和删除切片

- 单击切片：选择当前切片；
- `Shift` + 单击：加入或移出多选；
- 单击编辑区空白位置：清除选择；
- 选择 **删除切片** 后单击切片：删除该切片。

切片左上角编号表示从上到下的顺序。

### 6. 撤销和重做

- **撤销**：恢复上一步创建、删除或边界调整；
- **重做**：重新执行刚刚撤销的操作。

执行新的编辑操作后，已有重做记录会被清空。

### 7. 制作 EDM

完成切割后，点击右上角绿色的 **制作 EDM** 按钮。工具会：

1. 按从上到下的顺序裁切长图；
2. 将切片转换为 JPEG 图片；
3. 自动切换至上传切片模式；
4. 显示 Outlook 邮件预览。

随后可继续调整顺序、显示宽度和邮件主题，并生成 EML。

## 在 Outlook 中使用 EML

1. 找到浏览器下载的 `.eml` 文件；
2. 使用 Microsoft Outlook 打开；
3. 检查主题、图片宽度和切片顺序；
4. 添加收件人或其他正文内容；
5. 发送邮件。

正式发送前，建议先向桌面端和移动端测试邮箱发送一封测试邮件，确认图片加载、切片接缝和邮件宽度。

## 数据与输出说明

- 图片通过浏览器 `FileReader` 在本地读取。
- 长图切片通过 Canvas API 完成。
- 长图生成的切片为 JPEG，质量参数为 `0.9`。
- EML 图片通过 CID 内嵌，不依赖远程 URL。
- 邮件图片表格前会保留三行空白。
- 图片越多、尺寸越大，生成的 EML 文件也越大。

## 使用建议

- 文件名使用补零编号，例如 `edm_01.jpg`、`edm_02.jpg`。
- 尽量在纯色、留白或模块分隔处切片。
- 避免从文字、按钮、人物面部和复杂渐变中间切开。
- `15 cm` 可作为桌面邮件宽度的起始值，最终效果请以测试邮件为准。
- 在不影响清晰度的前提下压缩原始图片，以控制 EML 大小。

## 常见问题

### 页面一直停留在加载界面

检查网络是否能访问所需 CDN，并查看浏览器 Console 和 Network 面板。

### 图片初始顺序不正确

检查文件名中的第一个数字，或在预览区直接拖拽调整。

### 无法创建切片

新切片必须从未被已有切片占用的纵向区域开始，且不能与其他切片重叠。

### 边界无法继续拖动

边界受到图片范围、相邻切片和最小高度约束，这是为了避免越界和重叠。

### 预览图片超过预览框

使用预览区底部的横向滚动条。这不会改变最终导出的邮件宽度。

### 点击生成 EML 没有反应

确认至少存在一张切片图片，并检查浏览器是否阻止下载。

---

# English Guide

## Overview

Outlook EDM Maker is a browser-based tool for composing image-based EDM emails. You can combine pre-sliced images or divide one long design into horizontal slices, then export the result as an `.eml` file that can be opened in Microsoft Outlook.

The project is implemented as a single front-end file and requires no build step. Image reading, slicing, previewing, and email generation all happen locally in the browser; the application does not upload your images to a server.

## Features

- **Bilingual interface**: switch between Chinese and English with the button in the upper-right corner; the choice is remembered by the browser.
- **Upload Slices mode**: upload multiple images, sort them automatically, reorder them by dragging, set the email width, and generate an EML file.
- **Slice Long Image mode**: create, resize, and delete full-width horizontal slices with snapping, measurements, undo, and redo.
- **Outlook preview**: preview the EDM at its configured width and use horizontal scrolling for oversized content.
- **EML export**: embed images as CID resources so the generated email does not depend on remote image URLs.

## Requirements

Use a recent desktop browser, preferably:

- Microsoft Edge
- Google Chrome

The page loads these dependencies from CDNs:

- Tailwind CSS
- React 18
- React DOM 18
- Babel Standalone

> Images are processed locally, but the configured CDNs must be reachable when the page starts.

## Running the Project

### Open the file directly

Double-click `index.html`, or drag it into a browser window.

If the browser restricts scripts loaded from local files, use a local HTTP server instead.

### Run with Python (recommended)

From the project root:

```bash
python3 -m http.server 8080
```

Open:

```text
http://localhost:8080
```

### Run with Node.js

```bash
npx serve .
```

Open the URL printed in the terminal.

## Switching Languages

The interface starts in Chinese by default. Click **English** in the upper-right corner to switch to English, and click **中文** to switch back.

- The selected language is stored in browser local storage.
- The same language is restored the next time the page opens.
- If the subject still contains the system default, switching languages also translates that default subject.
- A subject entered by the user is never overwritten when the language changes.

## Workflow 1: Upload Pre-sliced Images

Use this workflow when your EDM has already been exported as multiple consecutive images.

### 1. Select Upload Slices

Click **Upload Slices** at the top of the page.

### 2. Enter the email subject

Enter a title in **Email Subject**. It is used both as the email subject and as the downloaded `.eml` filename.

### 3. Set the display width

Enter the image width in centimeters under **Size Settings**. The default is `15 cm`.

This changes only the rendered width in the final email. Original files are not resized, and image heights are calculated from their aspect ratios.

### 4. Upload images

Click **Upload multiple image slices** and select one or more files.

Sequential filenames are recommended:

```text
slice_01.jpg
slice_02.jpg
slice_03.jpg
```

The tool uses the first number in each filename for initial sorting. Files without a number are placed after numbered files.

### 5. Reorder and preview

In the Outlook preview, drag an image to a new position. The preview order is the final email order.

If the configured width is larger than the preview panel, use the horizontal scrollbar at the bottom of the preview.

### 6. Generate the EML file

After confirming the subject, width, and order, click **Generate EML**. The browser downloads an `.eml` file named after the email subject.

## Workflow 2: Slice a Long Image

Use this workflow when you have one complete long-form design.

### 1. Select Slice Long Image

Click **Slice Long Image** at the top of the page.

### 2. Upload the design

Click **Upload one long design image** and select an image. This mode handles one long image at a time; uploading again replaces the current image.

### 3. Create slices

Select **Slice Tool**, then start in a vertical region that is not already occupied by another slice:

1. Hold the left mouse button;
2. Drag upward or downward;
3. Release to create the slice.

While drawing:

- Every slice spans the full image width;
- A guide shows the current vertical position;
- A measurement label shows the source-pixel width and height;
- The edge snaps near image and existing slice boundaries;
- The range is constrained by neighboring slices and image edges;
- New slices cannot overlap existing slices;
- You may begin dragging from the gray area to either side of the image.

Starting inside an existing slice does not create a new slice.

### 4. Resize slice boundaries

With **Slice Tool** active, move the pointer near the top or bottom edge of a slice. The guide highlights and the cursor changes when an edge can be resized.

- Dragging a shared boundary resizes both adjacent slices;
- An independent edge cannot cross a neighboring slice;
- Minimum slice height is preserved;
- Snapping continues to apply during resizing;
- The active drag continues even if the pointer leaves the editor area.

### 5. Select and delete slices

- Click a slice to select it;
- `Shift` + click adds or removes it from the selection;
- Click blank editor space to clear the selection;
- Activate **Delete Slice**, then click a slice to remove it.

The number in the upper-left corner of each slice indicates its top-to-bottom order.

### 6. Undo and redo

- **Undo** restores the previous create, delete, or resize operation;
- **Redo** reapplies the most recently undone operation.

Performing a new edit clears the redo history.

### 7. Create the EDM

When slicing is complete, click the green **Create EDM** button. The application will:

1. Crop the long image from top to bottom;
2. Convert each slice to JPEG;
3. Switch automatically to Upload Slices mode;
4. Display the Outlook email preview.

You can then reorder slices, change the display width or subject, and generate the EML file.

## Using the EML File in Outlook

1. Locate the downloaded `.eml` file;
2. Open it with Microsoft Outlook;
3. Verify the subject, image width, and slice order;
4. Add recipients or additional email content;
5. Send the message.

Before a production send, send a test message to desktop and mobile mailboxes to verify image loading, slice seams, and overall width.

## Data and Output Details

- Images are read locally with the browser `FileReader` API.
- Long-image slicing uses the Canvas API.
- Generated long-image slices are JPEG files with a quality value of `0.9`.
- EML images are embedded with CID references and do not require remote URLs.
- Three blank lines are inserted before the image table in the email body.
- More or larger images produce a larger EML file.

## Recommendations

- Use zero-padded filenames such as `edm_01.jpg` and `edm_02.jpg`.
- Place slice boundaries in solid-color, whitespace, or natural module-separation areas.
- Avoid slicing through text, buttons, faces, or complex gradients.
- Use `15 cm` as a starting desktop email width and validate it with test emails.
- Compress source images when possible to keep the EML file size manageable.

## Troubleshooting

### The page remains on the loading screen

Verify that the required CDNs are reachable and inspect the browser Console and Network panels.

### Images are initially in the wrong order

Check the first number in each filename, or reorder the images directly in the preview.

### A new slice cannot be created

The drag must begin in a vertical area that is not occupied by an existing slice, and slices cannot overlap.

### A boundary stops moving

Boundaries are constrained by the image edges, neighboring slices, and the minimum slice height.

### The preview is wider than the panel

Use the horizontal scrollbar at the bottom of the preview. This does not change the exported email width.

### Generate EML does nothing

Make sure at least one image slice exists and verify that the browser is not blocking downloads.

---

## 项目结构 / Project Structure

```text
OutlookEDM/
├── index.html   # 页面、样式与应用逻辑 / UI, styles, and application logic
└── README.md    # 中英双语文档 / Bilingual documentation
```

## 技术栈 / Technology

- HTML5
- CSS / Tailwind CSS
- React 18
- Babel Standalone
- Canvas API
- FileReader API
- Blob / Object URL

无需安装依赖、编译或打包。所有核心功能均位于 `index.html` 中。

No dependency installation, compilation, or bundling is required. All core functionality is contained in `index.html`.
