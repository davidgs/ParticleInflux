# Integrating Particle with InfluxDB Cloud

If you followed the [previous tutorial](https://www.influxdata.com/resources/particle-ioandinfluxdb/) I presented a couple of years ago about integrating Particle.io with [InfluxDB](https://www.influxdata.com/products/influxdb-overview/) and were unhappy, or simply couldn't get it working, have I got a treat for you! Integrating Particle.io with [InfluxDB Cloud](https://cloud2.influxdata.com/signup) is very straightforward and requires no outside services or customizations outside of what Particle Cloud already offers. 

Here are the steps to get it all working:

1. Go to your [Particle.io Console](https://console.particle.io/) and click on the Integrations tab.
2. Click on New Integration, and choose Webhook.
3. Fill out the form! You need to know your event name, and it needs to be spelled exactly the same as it is in your on-device code!
4. You'll then enter the URL of your [InfluxDB Cloud]("https://cloud2.influxdata.com") instance. It might be different depending on the region you signed up for, which can be found on Load Data --> Client Libraries Page: 
   
   ```
   https://<your region>.<aws or gcp>.cloud2.influxdata.com/api/v2/write?org=YOUR_ORG&bucket=YOUR_BUCKET&precision=s
   ```
   
   You will need to know the name of your Organization and Bucket as well, which you can grab from the InfluxDB Cloud management interface.

![edit Integration screen][Console-1]

[Console-1]: https://www.influxdata.com/wp-content/uploads/influxdb-cloud-particle-edit-integration.png

5. Next you'll want to choose 'Custom Body' as your request format, and then expand the 'Advanced' setting as well. In there, you will insert the following:

![advanced settings][Console-2]

[Console-2]: https://www.influxdata.com/wp-content/uploads/Screen-Shot-2020-02-21-at-1.20.02-PM.png

   You can set whatever tags, if any, that you'd like, and then use the <a href="https://mustache.github.io/">'mustache' notation</a> to reference the Event Name and the Event Value, which will be used as the value name and value in InfluxDB.

6. Finally, you will need to add the Authorization Header exactly as below. The Authorization Header should have the value 'Token long-token-string-from-InfluxDBCloud' in it. This is the exact same header needed when accessing any of the [InfluxDB Cloud APIs](https://v2.docs.influxdata.com/v2.0/write-data/#example-api-write-request). You can then save your integration, and you're all set.

![authorization screen][Console-3]

[Console-3]: https://www.influxdata.com/wp-content/uploads/Screen-Shot-2020-02-21-at-1.20.15-PM.png

   Once you save your integration, you will see a page that tells you all the details of it:

![confirmation screen][Console-4]

[Console-4]: https://www.influxdata.com/wp-content/uploads/influxdb-cloud-particle-save-integration.png" 

   And below that, it even gives you some sample on-device code that will trigger the integration:

![sample code][Console-5]

[Console-5]: https://www.influxdata.com/wp-content/uploads/influxdb-cloud-particle-trigger-integration.png

And that's it! So simple!  