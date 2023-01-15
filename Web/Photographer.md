# Photographer

web.isangxcaution.xyz:20200


Made by smart_kang

사진의 metadata를 이용해서 flask LFI를 실행시키는 문제였다.
개인적으로 가장 재밌었던 web 문제

사진의 metadata 수정에는 exiftool을 이용했다.

```python
def thumbnailTemplate(thumbnail,camera_info,tags):
    template = '''
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <title>Image Analysis</title>
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
    </head>
    <body>
    <div class="container text-center" >
        <h1> Did you know that your image has senesitive information? </h1>
        <img src="data:image/jpeg;base64,{}" alt="No Thumbnail Image">

        <h4 class="mt-3">
        Your Camera is <u>{}</u> right?
        </h4>
        <hr>

        <h3> More Exif medatada </h3>
        <table class="table table-striped">
        <thead>
            <tr>
                <th scope="col">Key</th>
                <th scope="col">Value</th>
            </tr>
        </thead>
        <tbody>
            {{% for key,value in tags.items() %}}
                <tr>
                    <td>{{{{  key  }}}}</td>
                    <td>{{{{ value }}}}</td>
                </tr>
            {{% endfor %}}
        </tbody>
    </table>
    </div>
    </body>
    '''.format(thumbnail,camera_info)

    return render_template_string(template,tags=tags)
```
위 소스 코드에서 camera_info 부분을 이용했다.
```python
        if 'Image Make' in tags.keys() and 'Image Model' in tags.keys():
            camera_info = str(tags['Image Make']) + ' ' + str(tags['Image Model'])
            tags.pop('Image Make')
            tags.pop('Image Model')
```
camera_info 의 값은 Make와 Model Tag로 이루어져있기때문에 삽입할 코드를 적절히 나누어서 해당 Tag에 담아주면 된다. <br>
```python
        img = io.BytesIO(b_img)
```

자세한 Flask LFI 방법에 대해서는 [해당 문서 참조](https://payatu.com/blog/understanding-ssti/)
