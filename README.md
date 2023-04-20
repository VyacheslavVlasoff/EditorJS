<!DOCTYPE html>
<html>
    <head>
        <link href="css/style.css" rel="stylesheet" type="text/css">
        <script src="script/functions.js"></script>
        <script src="https://cdn.jsdelivr.net/npm/@editorjs/editorjs@latest"></script>
        <script src="https://cdn.jsdelivr.net/npm/@editorjs/header@latest"></script>
        <script src="https://cdn.jsdelivr.net/npm/@editorjs/raw"></script>
        <script src="https://cdn.jsdelivr.net/npm/@editorjs/simple-image@latest"></script>
        <script src="https://cdn.jsdelivr.net/npm/@editorjs/image@2.3.0"></script>
        <script src="https://cdn.jsdelivr.net/npm/@editorjs/checklist@latest"></script>
        <script src="https://cdn.jsdelivr.net/npm/@editorjs/list@latest"></script>
        <script src="https://cdn.jsdelivr.net/npm/@editorjs/embed@latest"></script>
        <script src="https://cdn.jsdelivr.net/npm/@editorjs/quote@latest"></script>
    </head>
    <body>
        <button id="save-button">Save</button>
        <div id="editorjs"></div>
        
        <script>
            const editor = new EditorJS({
                autofocus: true,
                tools: {
                    simagebg: MySimpleImage,
                    header: {
                        class: Header,
                        config: {
                            placeholder: 'Header...',
                            levels: [1, 2, 3, 4, 5, 6],
                            defaultLevel: 1
                        }
                    },
                    raw: RawTool,
                    simage: SimpleImage,
                    image: {
                        class: ImageTool,
                        config: {
                            endpoints: {
                                byFile: 'http://localhost:8008/uploadFile', // Your backend file uploader endpoint
                                byUrl: 'http://localhost:8008/fetchUrl', // Your endpoint that provides uploading by Url
                            }
                        }
                    },
                    checkList: {
                        class: Checklist,
                        inlineToolbar: true
                    },
                    list: {
                        class: List,
                        inlineToolbar: true,
                        config: {
                            defaultStyle: 'unordered'
                        }
                    },
                    embed: {
                        class: Embed,
                        config: {
                            services: {
                                youtube: true,
                                coub: true
                            }
                        }
                    },
                    quote: Quote
                },
                data: {
                    time: 1552744582955,
                    blocks: [
                        {
                            type: "paragraph",
                            data: { 
                                text: "Блок параграфа"
                            }
                        },
                    {
                        type: "simagebg",
                        data: {
                            url: "https://i.ytimg.com/vi/rz6w28wtAyU/maxresdefault.jpg",
                            withBorder: false,
                            withBackground: false,
                            stretched: false
                        }
                    }
                    ],
                    version: "2.11.10"
                }
            });

            const saveButton = document.getElementById('save-button');
        
            saveButton.addEventListener('click', () => {
              editor.save().then( savedData => {
                console.log(JSON.stringify(savedData, null, 4));
              })
            })
        </script>
    </body>
</html>
