## JSON
Javascript Object Notation，Javascript对象表示法，它是一种结构化数据格式。

1，与javascript对象字面量相比的不同之处   

没有声明变量（JSON中没有变量的概念）；  

没有末尾的分号。

注意：对象的属性必须加双引号。

* App.view.xml

```xml
<mvc:View
	controllerName="sap.ui.demo.wt.controller.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc">
	<Button
		text="Say Hello"
		press="onShowHello" />
	<Input
		value="{/recipient/name}"//value取自于recipient的name属性
		description="Hello {/recipient/name}"
		valueLiveUpdate="true"
		width="60%" />
</mvc:View>
```

* App.controller.js

```javascript
sap.ui.define([
   "sap/ui/core/mvc/Controller",
   "sap/m/MessageToast",
   "sap/ui/model/json/JSONModel"
], function (Controller, MessageToast, JSONModel) {
   "use strict";
   return Controller.extend("sap.ui.demo.wt.controller.App", {
      onInit : function () {//onInit类似构造函数，当一个controller被创建时会被调用
         // set data model on view
         var oData = {
            recipient : {
               name : "World"
            }
         };
         var oModel = new JSONModel(oData);
         this.getView().setModel(oModel);//将oModel创建一个Model并传给view
      },
      onShowHello : function () {
         MessageToast.show("Hello World");
      }
   });
});
```
* index.html

```html
<!DOCTYPE html>
<html>
   <head>
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta charset="utf-8">
      <title>Walkthrough</title>
      <script
         id="sap-ui-bootstrap"
         src="/resources/sap-ui-core.js"
         data-sap-ui-theme="sap_bluecrystal"
         data-sap-ui-libs="sap.m"
         data-sap-ui-compatVersion="edge"   //为了能够使用复杂的绑定语法
         data-sap-ui-preload="async" 
	 data-sap-ui-resourceroots='{
		"sap.ui.demo.wt": "./"
	}' >
      </script>
      <script>
         sap.ui.getCore().attachInit(function () {
			sap.ui.xmlview({
				viewName: "sap.ui.demo.wt.view.App"
			}).placeAt("content");
         });
      </script>
   </head>
   <body class="sapUiBody" id="content">
   </body>
</html>
```
