---
layout: post
title:      "How to Utilize Image Upload with your Heroku Application"
date:       2021-01-07 03:13:53 +0000
permalink:  how_to_utilize_image_upload_with_your_heroku_application
---

![](http://)

For one of my recent Rails projects I created an application that allowed users to create accounts, add pets to their accounts, and connect with other pet owners. I included a feature that allowed users to upload files for pet profile images. It seemed simple enough until I tried to deploy my app to Heroku. I immediately ran into an issue with Heroku's ephemeral file system. As stated by Heroku:

> Each dyno gets its own ephemeral filesystem, with a fresh copy of the most recently deployed code…
> …For example, this occurs any time a dyno is replaced due to application deployment and approximately once a day as part of normal dyno management.

Bad news for me. But lo and behold, Heroku recently released a new add-on called Simple File Upload. With this add-on you can upload files directly to cloud storage just with Heroku! Before we start implementing Simple File Upload to an existing Rails application, make sure you've completed the following prerequisites.

1. Update billing info for your Heroku account (Must have valid credit card on file).
2. Your Rails application must already be deployed on Heroku (if it's your first time deploying to Heroku, [here](https://medium.com/@kasiarosenb/deploying-your-rails-app-on-heroku-a2096dc40aac) is a great tutorial).

With those two steps out of the way, let's get started!


---

## Enable Simple File Upload for your Application

Navigate to the root directory of your application. Run the following command in your terminal.

`heroku addons:create simple-file-upload`

Next, add the below Javascript file to your application inside your <head> tags (make sure to update the API key).

```
<script src="https://app.simplefileupload.com/buckets/[your API key here].js"></script>
```
You can access your API key by running the following in your terminal:

```
heroku config:get SIMPLE_FILE_UPLOAD_KEY
```


---

## Edit your Form to use Simple File Upload
If you're using form_with you'll want to update it to appear as below:

```
<%= form_with model: @pet do |form| %>
```

Below the file_field form helper add the following:

```
<%= form.hidden_field :image, class: "simple-file-upload" %>
```

My finished form looks like this:

```
<%= form_with model: @pet, local: true do |form| %>
    <%= form.label :name, "Name", class: "label" %>
    <%= form.text_field :name, class: "input" %>

    <%= form.label :image, "Profile Image", class: "label" %>
    <%= form.file_field :image, class: "input" %>
    <%= form.hidden_field :image, class: "simple-file-upload" %>

    <%= form.submit %>
<% end %>
```

---

## Navigate to your Heroku App and View Your New Form
And you're done! If you view your form on Heroku it should now appear similar to this:

![](https://i.ibb.co/HBBbhqS/1-W-U9-EWAVy2d-ITG0y-IOL2-FQ.png)

Happy coding!

