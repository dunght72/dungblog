+++
categories = []
date = 2022-10-10T13:00:00Z
description = "Cách thêm ngôn ngữ Tiếng Việt để download phụ đề trên Subscene của Video Station"
draft = true
featured = false
featuredImage = "/uploads/1656001588_v8awn.png"
featuredImagePreview = "/uploads/1656001588_v8awn.png"
slug = "them-ngon-ngu-tieng-viet-vao-subscene-tren-video-station"
tags = []
title = "[Synology] Thêm ngôn ngữ Tiếng Việt vào Subscene trên Video Station"
toc = false

+++
Trên Video Station của Synology có plugin Subscene để tự động tìm kiếm và download phụ đề khá hay, nhưng rất tiếc, mặc định plugin này lại không có tiếng Việt để bạn lựa chọn. Bài viết dưới đây sẽ hướng dẫn bạn thêm Tiếng Việt vào option download nhé.

Dưới đây là cách làm:

\- Download đoạn mã Javascript từ đường link: [https://gist.github.com/the-unsoul/7f9ddfa60f4f1247c6f118fd55f05e17](https://gist.github.com/the-unsoul/7f9ddfa60f4f1247c6f118fd55f05e17 "https://gist.github.com/the-unsoul/7f9ddfa60f4f1247c6f118fd55f05e17") hoặc lưu đoạn code dưới đây thành file js

```javascript
(function() {
  var synoLang;
  var isSynoReady;

  var additional = {
    code : 'vie', // <== uses reference language list at the bottom and set the 'code' to the language you wanted
    label: 'Tiếng Việt' // <== 'label' can be anything you wanted. i.e. if set to 'New lang 123' you will see 'New lang 123' in the list
  }


  var overrideSupportedLanguage = function () {
      synoLang = SYNO.SDS.Utils.getSupportedLanguage();
      synoLang.push([additional.code, additional.label])
      SYNO.SDS.Utils.getSupportedLanguage = function () {
        return synoLang;
      }
  }

  var overrideSubtitleSet = function() {
      SYNO.SDS.VideoStation2.Setting.AdvancedPanel.SubtitleSet.LANGUAGE_MAPPING[additional.code] = additional.code;
      SYNO.SDS.VideoStation2.Setting.AdvancedPanel.SubtitleSet.EXTRA_LANGUAGE.push([additional.code, additional.label]);
  }

  var waitForSyno = setInterval(function () {

    try {
      var testAssignment = SYNO.SDS.VideoStation2.Setting.AdvancedPanel;
      isSynoReady = true;
    } catch (ex) {}

    if (!isSynoReady) {return;}

    clearInterval(waitForSyno);

    overrideSubtitleSet()
    overrideSupportedLanguage();

    console.log('[DONE] New language injected:', `'${additional.code}' '${additional.label}'`);
  }, 500)

})();


// this is refference for language support list in subscene
// 'Albanian'             : {'id': 1, '3let': 'alb', '2let': 'sq', 'name': 'Albanian'},
// 'Arabic'               : {'id': 2, '3let': 'ara', '2let': 'ar', 'name': 'Arabic'},
// 'Big 5 code'           : {'id': 3, '3let': 'chi', '2let': 'zh', 'name': 'Chinese'},
// 'Brazillian Portuguese': {'id': 4, '3let': 'por', '2let': 'pb', 'name': 'Brazilian Portuguese'},
// 'Bulgarian'            : {'id': 5, '3let': 'bul', '2let': 'bg', 'name': 'Bulgarian'},
// 'Chinese BG code'      : {'id': 7, '3let': 'chi', '2let': 'zh', 'name': 'Chinese'},
// 'Croatian'             : {'id': 8, '3let': 'hrv', '2let': 'hr', 'name': 'Croatian'},
// 'Czech'                : {'id': 9, '3let': 'cze', '2let': 'cs', 'name': 'Czech'},
// 'Danish'               : {'id': 10, '3let': 'dan', '2let': 'da', 'name': 'Danish'},
// 'Dutch'                : {'id': 11, '3let': 'dut', '2let': 'nl', 'name': 'Dutch'},
// 'English'              : {'id': 13, '3let': 'eng', '2let': 'en', 'name': 'English'},
// 'Estonian'             : {'id': 16, '3let': 'est', '2let': 'et', 'name': 'Estonian'},
// 'Farsi/Persian'        : {'id': 46, '3let': 'per', '2let': 'fa', 'name': 'Persian'},
// 'Finnish'              : {'id': 17, '3let': 'fin', '2let': 'fi', 'name': 'Finnish'},
// 'French'               : {'id': 18, '3let': 'fre', '2let': 'fr', 'name': 'French'},
// 'German'               : {'id': 19, '3let': 'ger', '2let': 'de', 'name': 'German'},
// 'Greek'                : {'id': 21, '3let': 'gre', '2let': 'el', 'name': 'Greek'},
// 'Hebrew'               : {'id': 22, '3let': 'heb', '2let': 'he', 'name': 'Hebrew'},
// 'Hungarian'            : {'id': 23, '3let': 'hun', '2let': 'hu', 'name': 'Hungarian'},
// 'Icelandic'            : {'id': 25, '3let': 'ice', '2let': 'is', 'name': 'Icelandic'},
// 'Indonesian'           : {'id': 44, '3let': 'ind', '2let': 'id', 'name': 'Indonesian'},
// 'Italian'              : {'id': 26, '3let': 'ita', '2let': 'it', 'name': 'Italian'},
// 'Japanese'             : {'id': 27, '3let': 'jpn', '2let': 'ja', 'name': 'Japanese'},
// 'Korean'               : {'id': 28, '3let': 'kor', '2let': 'ko', 'name': 'Korean'},
// 'Lithuanian'           : {'id': 43, '3let': 'lit', '2let': 'lt', 'name': 'Lithuanian'},
// 'Malay'                : {'id': 50, '3let': 'may', '2let': 'ms', 'name': 'Malay'},
// 'Norwegian'            : {'id': 30, '3let': 'nor', '2let': 'no', 'name': 'Norwegian'},
// 'Polish'               : {'id': 31, '3let': 'pol', '2let': 'pl', 'name': 'Polish'},
// 'Portuguese'           : {'id': 32, '3let': 'por', '2let': 'pt', 'name': 'Portuguese'},
// 'Romanian'             : {'id': 33, '3let': 'rum', '2let': 'ro', 'name': 'Romanian'},
// 'Russian'              : {'id': 34, '3let': 'rus', '2let': 'ru', 'name': 'Russian'},
// 'Serbian'              : {'id': 35, '3let': 'scc', '2let': 'sr', 'name': 'Serbian'},
// 'Slovak'               : {'id': 36, '3let': 'slo', '2let': 'sk', 'name': 'Slovak'},
// 'Slovenian'            : {'id': 37, '3let': 'slv', '2let': 'sl', 'name': 'Slovenian'},
// 'Spanish'              : {'id': 38, '3let': 'spa', '2let': 'es', 'name': 'Spanish'},
// 'Swedish'              : {'id': 39, '3let': 'swe', '2let': 'sv', 'name': 'Swedish'},
// 'Thai'                 : {'id': 40, '3let': 'tha', '2let': 'th', 'name': 'Thai'},
// 'Turkish'              : {'id': 41, '3let': 'tur', '2let': 'tr', 'name': 'Turkish'},
// 'Vietnamese'           : {'id': 45, '3let': 'vie', '2let': 'vi', 'name': 'Vietnamese'}
```

* Mở Video Station bằng Google Chrome


* Bấm F12 để mở Dev Tools, sau đó chọn Console


* Dán đoạn mã trên vào và Enter (Có thể sửa dòng 5&6, code và label thành ngôn ngữ khác nếu muốn, như các dòng comment ở phía dưới)
* Đợi một chút, trên màn hình sẽ hiển thị kết như bên dưới

> \[DONE\] New language injected: 'vie' 'Tiếng Việt'

* Bây giờ vào Setting trên Video Station ->  Advance -> Chọn Tiếng Việt

  ![](/uploads/1656001419_tl82i.png)
* Tải lại trang, vậy là bây giờ bạn đã có thể tải phụ đề bằng tiếng Việt rồi đó

  ![](/uploads/1656001588_v8awn.png)

Lưu ý: Mỗi khi bạn thay đổi cấu hình của Subscene trên Video Station thì phải làm lại từ đầu nhé. Chúc các bạn thành công

**Credit thuộc về:** Linh Pham @theuns