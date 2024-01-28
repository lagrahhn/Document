用于获取可输入元素，如输入框，选择框，单选按钮，下拉框，鼠标点击，键盘输入，快捷键，上传文件和获取焦点等。

### 文本输入
查看Locator.FillAsync的[详细用法](https://playwright.dev/dotnet/docs/api/class-locator#locator-fill)
```c#
// Text input
await page.GetByRole(AriaRole.Textbox).FillAsync("Peter");

// Date input
await page.GetByLabel("Birth date").FillAsync("2020-02-02");

// Time input
await page.GetByLabel("Appointment time").FillAsync("13-15");

// Local datetime input
await page.GetByLabel("Local time").FillAsync("2020-03-02T05:15");
```

### 选择框和单选按钮
查看Locator.SetCheckedAsync的[详细用法](https://playwright.dev/dotnet/docs/api/class-locator#locator-set-checked)

```c#
// Check the checkbox
await page.GetByLabel("I agree to the terms above").CheckAsync();

// Assert the checked state
await Expect(page.GetByLabel("Subscribe to newsletter")).ToBeCheckedAsync();

// Select the radio button
await page.GetByLabel("XL").CheckAsync();
```

### 下拉框
查看Locator.SelectOptionAsync的[详细用法](https://playwright.dev/dotnet/docs/api/class-locator#locator-select-option)

```c#
// Single selection matching the value or label
await page.GetByLabel("Choose a color").SelectOptionAsync("blue");

// Single selection matching the label
await page.GetByLabel("Choose a color").SelectOptionAsync(new SelectOptionValue { Label = "blue" });

// Multiple selected items
await page.GetByLabel("Choose multiple colors").SelectOptionAsync(new[] { "blue", "green", "red" });
```
### 鼠标点击

