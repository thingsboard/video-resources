# Introduction

These are the learning materials for the **How to Customize ThingsBoard with White Labeling** video.
During this lesson, you will learn how to:

- How to customize the title, logo, and primary color scheme of your ThingsBoard instance
- How to create a personalized login page with your own branding
- How to use advanced CSS settings to create a unique interface style
- How to add your own custom domain name
- How to edit and personalize email templates

# CSS for General page

```
/*icon color*/

.mat-icon.notranslate.material-icons.mat-ligature-font.mat-icon-no-color.ng-star-inserted {
    fill: #9F31FF;
    color: #9F31FF;
}

.mat-icon.notranslate.mat-icon-no-color.ng-star-inserted {
    fill: #9F31FF;
}

/*menu gradient*/

.tb-side-menu {
    background: linear-gradient(0deg, #1F263C, #381855, #1F263C);
}

/* Improve scrollbar for menu and dashboard items */
mat-toolbar::-webkit-scrollbar, div::-webkit-scrollbar,
ng-component::-webkit-scrollbar {
  width: 7px !important;
  height: 7px !important;
}
mat-toolbar::-webkit-scrollbar-track, div::-webkit-scrollbar-track,
ng-component::-webkit-scrollbar-track {
  background-color: grey !important;
  background-image: linear-gradient(grey,grey,grey);
}
mat-toolbar::-webkit-scrollbar-thumb, div::-webkit-scrollbar-thumb,
ng-component::-webkit-scrollbar-thumb  {
  background-color: white !important;
      background-image: linear-gradient(white);
  border-radius: 7px !important;
  border: 0.1rem outset grey;
}
```

# CSS for Login:

```
.mat-mdc-card.mdc-card{box-shadow: 0px 0px 0px 0px grey;
    border-radius: 15px;
    border: 1px solid white;
    box-shadow: #9F31FF 0px 12px 55px, white
 0px -12px 55px, #9F31FF 0px 4px 6px, #9F31FF 0px 6px 12px, #9F31FF 0px -3px 5px;
}
```
