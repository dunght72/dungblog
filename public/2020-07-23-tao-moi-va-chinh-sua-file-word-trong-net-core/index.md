# Tạo mới và chỉnh sửa file Word trong .NET Core

Bài viết dưới đây hướng dẫn tạo và chỉnh sửa file Word trong ứng dụng .Net Core sử dụng WYSIWYG editor và Aspose.Word
![Sửa file Word trong .Net Core](https://cdn.shortpixel.ai/client/q_glossy,ret_img/https://blog.aspose.com/wp-content/uploads/sites/2/2020/04/ASP.NET-Word-Editor.jpg)

* Bước 1: Tạo mới 1 ứng dụng ASP.NET Core Web Application (MVC)
* Bước 2: Download WYSIWYG editor và đặt trong wwwroot
* Bước 3: Mở Nuget Package Manager, tìm kiếm và cài đặt Aspose.Words for .NET package.
* Bước 4: Thêm đoạn code sau vào file index.cshtml

```javascript
@{
    ViewData["Title"] = "Word Editor in ASP.NET";
}
<div class="row">
    <div class="col-md-12">
        <form asp-controller="Home" asp-action="UploadFile" method="post" class="form-inline"
              enctype="multipart/form-data">
            <br />
            <div class="form-group">
                <input type="file" name="file" accept=".doc, .docx" class="form-control custom-file-input" />
            </div>
            <div class="form-group">
                <button type="submit" class="form-control btn btn-primary">Open</button>
            </div>
            <div class="form-group" style="position:relative; float :right">
                <button type="button" id="download" class="form-control btn btn-success" value="Save and Download">Save and Download</button>
            </div>
        </form>
        <br />
        <form method="post" asp-action="Index" id="formDownload">
            <textarea name="editor" id="editor" rows="80" cols="100">
                @if (ViewBag.HtmlContent == null)
                 {
                    <p>Write something or open an existing Word document. </p>
                 }
                 else
                 {
                     @ViewBag.HtmlContent;
                 }
                </textarea>
        </form>
    </div>
</div>
<!-- suneditor -->
<link href="~/suneditor/dist/css/suneditor.min.css" rel="stylesheet">
<!-- suneditor -->
<script src="~/suneditor/dist/suneditor.min.js"></script>
<script>
    var suneditor = SUNEDITOR.create('editor', {
        display: 'block',
        width: '100%',
        height: '30%',
        popupDisplay: 'full',
        buttonList: [
            ['font', 'fontSize', 'formatBlock'],
            ['paragraphStyle', 'blockquote'],
            ['bold', 'underline', 'align', 'strike', 'subscript', 'superscript', 'horizontalRule', 'list'],
            ['table', 'link', 'image'],
            ['align', 'horizontalRule', 'list', 'lineHeight'],
            ['codeView']
        ],
        placeholder: 'Start typing something...'
    });
</script>
<script>
    $(document).ready(function () {
        $("#download").click(function () {
            suneditor.save();
            $("#formDownload").submit();
        });
    });
</script>
```

* Bước 5: Thêm đoạn code dưới đây vào file HomeController.cs

```javascript
[HttpPost]
public FileResult Index(string editor)
{
	try
	{
		// Create a unique file name
		string fileName = Guid.NewGuid() + ".docx";
		// Convert HTML text to byte array
		byte[] byteArray = Encoding.UTF8.GetBytes(editor.Contains("<html>") ? editor : "<html>" + editor + "</html>");
		// Generate Word document from the HTML
		MemoryStream stream = new MemoryStream(byteArray);
		Document Document = new Document(stream);
		// Create memory stream for the Word file
		var outputStream = new MemoryStream();
		Document.Save(outputStream, SaveFormat.Docx);
		outputStream.Position = 0;
		// Return generated Word file
		return File(outputStream, System.Net.Mime.MediaTypeNames.Application.Rtf, fileName);
	}
	catch (Exception exp)
	{
		return null;
	}
}
[HttpPost]
public ViewResult UploadFile(IFormFile file)
{
	// Set file path
	var path = Path.Combine("wwwroot/uploads", file.FileName);
	using (var stream = new FileStream(path, FileMode.Create))
	{
		file.CopyTo(stream);
	}
	// Load Word document
	Document doc = new Document(path);
	var outStream = new MemoryStream();
	// Set HTML options
	HtmlSaveOptions opt = new HtmlSaveOptions();
	opt.ExportImagesAsBase64 = true;
	opt.ExportFontsAsBase64 = true;
	// Convert Word document to HTML
	doc.Save(outStream, opt);
	// Read text from stream
	outStream.Position = 0;
	using(StreamReader reader = new StreamReader(outStream))
	{
		ViewBag.HtmlContent = reader.ReadToEnd();
	}
	return View("Index");
}
```

* Bước 6: Build và chạy thử chương trình.
  
---

