Verndale Enforce Language Version Customizations for Fallback in Sitecore

Purpose
Potentially move the check for enforce language version into a later process (httpBeginRequest), 
disabled blank content even when enforce version presence is off, 
add ability to enforce an item exists for a specific region without using language versions.

Compatibility
The codebase is compatible with Sitecore 6.6.x releases and at least through Sitecore 7.2.x.
This assumes you are using the latest version of the Partial Language Fallback Module
http://marketplace.sitecore.net/en/Modules/Language_Fallback.aspx

How to build code and deploy the solution
1. When using the fallback module, make sure to compile the source code to get the dll, do not use the one within the package.

2. Download and unzip the Verndale.SharedSource.zip from this repository, it contains a class library
3. The important file in this are ItemLanguageValidation.cs, RegionValidationModule.cs, LanguageHelper.cs

4. Download the App_Config folder, there are necessary updates within Sitecore.SharedSource.PartialLanguageFallback.config.example
You can use the whole thing or take the parts from it that you need and add to your fallback.config
It contains an additional class to be used in the httpRequestBegin pipeline for checking for language version

5. Download the web.config example, there are two places in it that register the RegionValidationModule
this is used for checking for a field value of an item against a Session variable

Testing
1. Set the pageNotFoundGUID in the fallback.config site node for your site to your 404 page guid
2. Add a new treelist field to a page template: Limit To Countries, where user can select countries
3. Add ability for user to select one of these countries on the website and save into session variable, eg Session["Country Code"]
4. Set a Content item to limit to a specific country and then select a different country on the front-end, try to go to that page
5. Should redirect to your 404 page

Review the blog series about Partial Language Fallback on Sitecore, http://www.sitecore.net/en-gb/Learn/Blogs/Technical-Blogs/Elizabeth-Spranzani.aspx
