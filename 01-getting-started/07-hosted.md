# What is Directus Hosted?

## Directus Hosted is a highly scalable DBaaS (Database as a Service) platform for developers looking to easily give their clients an intuitive cloud-based interface for managing app/website content.

With a Directus Hosted account you can manage all your instances in one place, creating new Directus instances in seconds. Simply choose a name and size for your instance and within seconds you'll have a new SQL database ready to completely customize with your project's specific data architecture. Use the dynamic RESTful API to pull data into your app or website – or just use Directus as a standalone tool, similar to FileMaker. Either way, an unlimited number of users can upload files and manage database content, all based on granular group permissions.

### Your Account Dashboard
From here you can manage your account info, including your email, password, and payment details. From this panel you can also review your account's billing history, see any outstanding balance you might have, and close your account.

### Creating Instances
Once you have added payment info into your account you can easily and quickly add new instances. Just click on the "Create Instance" button in the header, fill in an instance name, and choose a plan – that's it. Names should be lowercase alphanumeric with dashes instead of spaces – choose your instance name carefully as that will determine your database name and API URL. It should only take a few second for your database and Directus CMS to be set up. Then, once you've created a schema and content, your dynamic API will be available.

### Managing Instances
Once you've created a few instances, you can easily manage them all in one place from the Instances section. In addition to changing your instance's plan (resizing), you will also be presented with other details, including:

* Table Count
* User Count
* Total Item Count
* Used & Available Asset Storage
* Used & Available Asset Bandwidth
* Used & Available Monthly API Requests
* Used & Available Monthly API Bandwidth

You will also be able to see all of your API users/keys listed here. Each Directus user has an associated API key that inherits its data privileges. Keys can be be updated within the instance's Directus Users section.

### Deleting Instances
You can delete instances from their detail page. There are three levels of confirmation to ensure you do not accidentally destroy instances. The following is permanently destroyed when deleting an instance:

* The database
* All data and content within the database
* The Directus CMS
* All associated assets
* All API endpoints (404)
