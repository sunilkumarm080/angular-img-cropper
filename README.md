
# lucida-img-cropper

This is an adapatation of Angular 1 image cropper from: https://github.com/AllanBishop/angular-img-cropper
An image cropping tool for AngularJS. Features a rectangular crop area. The crop area's aspect ratio can be enforced during dragging.
The crop image can either be 1:1 or scaled to fit an area.

## Install from NPM

```
    npm i lucida-img-cropper --save
```

## Screenshot

![Screenshot](https://raw.githubusercontent.com/cstefanache/cstefanache.github.io/master/assets/img/cropper.png "Screenshot")

## Testing

```
    npm install
    npm run all
```

## Example usage

```typescript
import {Component} from 'angular2/core';
import {ImageCropperComponent, CropperSettings} from 'ng2-img-cropper';


@Component({
    selector: 'test-app',
    template: `<div>
        <img-cropper [image]="data" [settings]="cropperSettings"></img-cropper><br>
        <img [src]="data.image" [width]="cropperSettings.croppedWidth" [height]="cropperSettings.croppedHeight">
    </div>`,
    declarations: [ImageCropperComponent]
})
export class AppComponent {
    data: any;
    cropperSettings: CropperSettings;

    constructor() {

        this.cropperSettings = new CropperSettings();
        this.cropperSettings.width = 100;
        this.cropperSettings.height = 100;
        this.cropperSettings.croppedWidth = 100;
        this.cropperSettings.croppedHeight = 100;
        this.cropperSettings.canvasWidth = 400;
        this.cropperSettings.canvasHeight = 300;

        this.data = {};

    }
}

```

Checkout this [sample plunker](https://embed.plnkr.co/VFwGvAO6MhV06IDTLk5W/)


## Settings

* **canvasWidth**:*number* - Canvas DOM Element width
* **canvasHeight**:*number* - Canvas DOM Element height
* **width**:*number* - Crop Width
* **height**:*number* - Crop Height
* **minWidth**:*number* - Minimum crop Width
* **minHeight**:*number* - Minimum crop height
* **croppedWidth**:*number* - Resulting image width
* **croppedHeight**:*number* - Resulting image height
* **touchRadius**:*number* - (default: 20) Touch devices radius for the corner markers
* **centerTouchRadius**:*number* (default: 20) - Touch devices radius for the drag center marker
* **minWithRelativeToResolution**:*boolean* - (default: true) By default the resulting image will be cropped from original image. If false, it will be cropped from canvas pixels
* **noFileInput**:*boolean* - (default: false) - hides the file input element from cropper canvas.
* **cropperDrawSettings**:*CropperDrawSettings* - rendering options
    * **strokeWidth**:*number* - box/ellipsis stroke width
    * **strokeColor**:*string* - box/ellipsis stroke color
* **allowedFilesRegex**:*RegExp* - (default: /\.(jpe?g|png|gif)$/i) - Regex for allowed images
* **preserveSize**:*boolean* - will not scale the resulting image to the croppedWidth/croppedHeight and will output the exact crop size from original
* **fileType**:*string* - if defined all images will be converted to desired format. sample: cropperSample.fileType = 'image/jpeg'
* **compressRatio**:*number* (default: 1.0) - default compress ratio
* **dynamicSizing**: (default: false) - if true then the cropper becomes responsive - might introduce performance issues on resize;
* **cropperClass**: string - set class on canvas element;
* **croppingClass**: string - appends class to cropper when image is set (#142);
* **resampleFn**: Function(canvas) - function used to resample the cropped image (#136); - see example #3 from runtime sample app
* **cropOnResize**:*boolean* (default: true) - if true the cropper will create a new cropped Image object immediately when the crop area is resized
* **markerSizeMultiplier**:*number* (default: 1) - A variable that control the corner markers' size
* **showCenterMarker**:*boolean* (default: true) - if true, the drag center marker is visible

## Customizing Image cropper

Replacing component file input:

```html
<div class="file-upload">
    <span class="text">upload</span>
    <input id="custom-input" type="file" (change)="fileChangeListener($event)">
</div>
<img-cropper #cropper [image]="data" [settings]="cropperSettings"></img-cropper>
<br>
<span class="result rounded" *ngIf="data.image" >
    <img [src]="data.image" [width]="cropperSettings.croppedWidth" [height]="cropperSettings.croppedHeight">
</span>
```

```typescript

data:any;

@ViewChild('cropper', undefined)
cropper:ImageCropperComponent;

constructor() {
    this.cropperSettings = new CropperSettings();
    this.cropperSettings.noFileInput = true;
    this.data = {};
}

fileChangeListener($event) {
    var image:any = new Image();
    var file:File = $event.target.files[0];
    var myReader:FileReader = new FileReader();
    var that = this;
    myReader.onloadend = function (loadEvent:any) {
        image.src = loadEvent.target.result;
        that.cropper.setImage(image);

    };

    myReader.readAsDataURL(file);
}


```



# Changelog

### Release 0.0.1
 - Defualt Cropper Size change





