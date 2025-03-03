# Introduction

These are the learning materials for the **first practical video** of the **ThingsBoard CE course**.
During this lesson, you will learn how to:
- Add your first **asset** with the corresponding **attributes**.
- Create first **dashboard** with the **custom Information card widget**.
- Personalize the **dashboard** and **Card widget appearence** with **code**.

# Adding asset

To add a new asset, go to the **Entities** section > **Assets**, and then select the **`+`** icon > **Add new asset**. Then enter the asset name and create the corresponding asset profile.

| Name          | Asset profile  |
| :----------   | :---------     |
| `Office A`    | office         |


# Adding attributes

To add a new attribute, select the office, go to the **Attributes** tab, and select the **`+`** icon. Enter the correspoding key, select the value type, and enter the value itself:

| Key            | Value type     | Value                 |
| :----------    | :---------     | :---------------------| 
| `address`      | String         | 645 5th Ave, New York |
| `floor`        | Integer        | 3                     |
| `email`        | String         | office.a@mail.test    |
| `phone`        | String         | +1 121 333 4455       |
| `officeManager`| String         | Emma Johnson          |


# Configuring Information card widget

To customize the Information card widget with code:
- Navigate to the **Appearance** tab and paste the code in the corresponding **Markdown/HTML pattern** window:

    ```
    # Information on office
     - **Address**: ${address}
     - **Floor**: ${floor:0}
     - **Office manager**: ${officeManager}
     - **Phone**: ${phone}
     - **Email**: ${email}

    ```


- To further beautify the widget, turn on the **Use markdown/HTML value function** option. In the corresponding window, add the value function:

    ```
    if (data.length) {
        
        const information = {
            entityName: data[0].entityName ? data[0].entityName : 'Not found',
            officeAttributesField: {
                floor: data[0].floor ? data[0].floor : 'Not found',
                officeManager: data[0].officeManager ? data[0].officeManager : 'Not found',
                phone: data[0].phone ? data[0].phone : 'Not found',
                email: data[0].email ? data[0].email : 'Not found',
                address: data[0].address ? data[0].address : 'Not found'
            }
        }; 
        
        const attributesNotFound = Object.values(information.officeAttributesField).every(value => value === 'Not found');
        
        if (attributesNotFound) {
            return '<div class="no-data-card">' +
                       `<h1 class="card-title">Information on office</h1>` +
                        '<div class="no-data-block">' + 
                            '<div class="no-data-content">' +
                                '<div><svg xmlns="http://www.w3.org/2000/svg" width="81" height="80" viewBox="0 0 81 80" fill="none"><path d="M14.8203 46.1166C16.6985 46.0291 18.2877 45.3003 19.588 43.9301C20.8883 42.56 21.5529 40.9274 21.5529 39.0325C21.5529 40.9274 22.1886 42.56 23.4889 43.9301C24.7892 45.3003 26.3784 46.0291 28.2566 46.1166C26.3784 46.204 24.7892 46.9328 23.4889 48.303C22.8602 48.9489 22.3653 49.7146 22.0329 50.5555C21.7005 51.3963 21.5374 52.2955 21.5529 53.2006C21.5529 51.3057 20.9172 49.6732 19.588 48.303C18.2877 46.9328 16.6985 46.204 14.8203 46.1166ZM21.5529 25.1267C25.1937 24.9518 28.2855 23.5234 30.8283 20.8413C33.371 18.1593 34.6424 14.9817 34.6424 11.2793C34.6424 14.9817 35.9138 18.1593 38.4566 20.8413C40.9994 23.5234 44.0912 24.9227 47.7609 25.1267C45.3626 25.2434 43.1665 25.9139 41.1439 27.1966C39.1501 28.4501 37.5608 30.141 36.3761 32.24C35.2203 34.3389 34.6424 36.5837 34.6424 39.0325C34.6424 35.3301 33.371 32.1234 30.8283 29.4413C28.2855 26.7301 25.1937 25.3017 21.5529 25.1267ZM31.1461 56.524C33.8912 56.4074 36.2317 55.3288 38.1387 53.3172C40.0458 51.3057 40.9994 48.9152 40.9994 46.1166C40.9994 48.9152 41.9529 51.3057 43.86 53.3172C45.7671 55.3288 48.0787 56.4074 50.8237 56.524C48.0787 56.6406 45.7671 57.7193 43.86 59.7308C41.9529 61.7423 40.9994 64.1328 40.9994 66.9315C40.9994 64.1328 40.0458 61.7423 38.1387 59.7308C36.316 57.7765 33.8041 56.6245 31.1461 56.524ZM50.8237 42.7057C53.5688 42.5891 55.8804 41.5105 57.7875 39.4989C59.6946 37.4874 60.6192 35.0969 60.6192 32.2691C60.6192 35.0678 61.5728 37.4583 63.4799 39.4698C65.3869 41.4813 67.7274 42.56 70.4725 42.6766C67.7274 42.7932 65.3869 43.8718 63.4799 45.8834C61.5728 47.8949 60.6192 50.2854 60.6192 53.084C60.6192 50.2854 59.6657 47.8949 57.7875 45.8834C55.8804 43.901 53.5688 42.8223 50.8237 42.7057Z" fill="#00695C" fill-opacity="0.4"/></svg></div>' +
                                '<p class="no-data-title">There is no information about the office</p>' +     
                            '</div>' +
                        '</div>' +
                   '</div>';            
        } else {
            return '<div class="card">' +
                       `<h1 class="card-title">Information on office</h1>` +
                       '<div class="attributes">' +
                            '<div class="attribute_container">' +
                                '<div class="icon_wrapper">' +
                                    '<tb-icon class="icon" color="primary" matButtonIcon>place</tb-icon>' +
                                '</div>' +
                                '<div class="attribute_content">' +
                                    `<p class="attribute">${information.officeAttributesField.address}</p>` +
                                    '<span class="attribute_label">Address</span>' +
                                '</div>' +
                            '</div>' +
                            '<div class="attribute_container">' +
                                '<div class="icon_wrapper">' +
                                    '<tb-icon class="icon" color="primary" matButtonIcon>mdi:floor-plan</tb-icon>' +
                                '</div>' +
                                '<div class="attribute_content">' +
                                    `<p class="attribute">${information.officeAttributesField.floor}</p>` +
                                    '<span class="attribute_label">Floor</span>' +
                                '</div>' +
                            '</div>' +
                            '<div class="attribute_container">' +
                                '<div class="icon_wrapper">' +
                                    '<tb-icon class="icon" color="primary" matButtonIcon>person</tb-icon>' +
                                '</div>' +
                                '<div class="attribute_content">' +
                                    `<p class="attribute">${information.officeAttributesField.officeManager}</p>` +
                                    '<span class="attribute_label">Office manager</span>' +
                                '</div>' +
                            '</div>' +
                            '<div class="attribute_container">' +
                                '<div class="icon_wrapper">' +
                                    '<tb-icon class="icon" color="primary" matButtonIcon>call</tb-icon>' +
                                '</div>' +
                                '<div class="attribute_content">' +
                                    `<p class="attribute">${information.officeAttributesField.phone}</p>` +
                                    '<span class="attribute_label">Phone</span>' +
                                '</div>' +
                            '</div>' +
                            '<div class="attribute_container">' +
                                '<div class="icon_wrapper">' +
                                    '<tb-icon class="icon" color="primary" matButtonIcon>mail_outline</tb-icon>' +
                                '</div>' +
                                '<div class="attribute_content">' +
                                    `<p class="attribute" style="word-break:break-all">${information.officeAttributesField.email}</p>` +
                                    '<span class="attribute_label">Email</span>' +
                                '</div>' +
                            '</div>' +
                       '</div>' +
                   '</div>';          
        }    
    }

    ```

- After this step, go to the **Markdown/HTML CSS** section and paste the following code there:

    ```
    .card, .no-data-card {
        padding: 0px;
        height: 100%;
    }
    .card-title {
        position: sticky;
        top: 0;
        z-index: 2;
        font-size: 16px;
        letter-spacing: 0.25px;
        padding: 16px;
    }
    .attribute_container {
        display: flex;
        align-items: center;
        gap: 20px;
        padding: 16px;
        border-bottom: 1px solid #0000000d;
    }
    .icon {
        z-index: 1;
    }
    .icon_wrapper {
        display: flex;
        position: relative;
        align-items: center;
        padding: 8px;
        border: 1px solid var(--tb-primary-100, #305680);
        border-radius: 4px;
    }
    .icon_wrapper:before {
        content: '';
        z-index: 0;
        position: absolute;
        opacity: 0.1;
        background-color: var(--tb-primary-200, #305680);
        width: 100%;
        height: 100%;
        left: 0;
        top: 0;
    }
    .attribute, .attribute_label {
        font-size: 14px;
        line-height: 20px;
    }
    .attribute_label {
        color: #00000061;
    }
    .no-data-card {
        display: flex;
        flex-direction: column;
    }
    .no-data-block {
        display: flex;
        flex-direction: column;
        justify-content: center;
        height: 100%;
        max-width: 345px;
        padding: 0 15px;
        margin: 0 auto;
        text-align: center;
    }
    .no-data-content {
        transform: translateY(-30%);
    }
    .no-data-block p {
        font-weight: 500;
    }
    .no-data-title {
        color: rgba(0, 0, 0, 0.54);
    }
    .no-data-subtitle {
        font-size: 13px;
        color: rgba(0, 0, 0, 0.38);
    }
    
    ```

# Setting dashboard background image

To add a new background image:
- Select the **Layouts** > **Gear** icon.
- In the **Background image** section, select **Browse from gallery** > **Upload image**.
- Drag & drop the image or upload it from your computer.
  
    - The [image](resources/office-room.jpg) we use in this tutorial.
      
- Save the changes.

# Customizing dashboard appearence

To customize the dashboard appearence:

- Select the **Settings** icon and go to the **Advanced settings** section. 
- In the **Dashboard CSS** section, paste the following code:
  
    ```
    .tb-widget-container > .tb-widget {
        border-radius: 8px;
        box-shadow: 0px 4px 10px rgba(23, 33, 90, 0.5);
    }
    ```
- Save the changes.
