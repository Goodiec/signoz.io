---
title: Feature in Spotlight - Logs Explorer [Launch Week Day 1] 🪵
slug: launch-week-1-day-1
date: 2024-02-26
tags: [OpenTelemetry, SigNoz]
authors: [ankit_anand]
description: Welcome to SigNoz Launch Week 1.0.This is our first launch week, and we’re excited to introduce you to some cool new features in SigNoz. The feature in spotlight for Day 1 is our new Logs Explorer...
image: /img/events/launch-week-1/launch-week-day-1-cover.webp
hide_table_of_contents: false
toc_min_heading_level: 2
toc_max_heading_level: 2
keywords:
  - launch week
  - day 1
  - logs explorer
  - signoz
  - observability
---

import { LiteYoutubeEmbed } from "react-lite-yt-embed";

<head>
  <link rel="canonical" href="https://signoz.io/newsroom/launch-week-1-day-1/"/>
   <meta property="og:image" content="https://signoz.io/img/events/launch-week-1/launch-week-day-1-cover.webp"/>
  <meta name ="twitter:image" content="https://signoz.io/img/events/launch-week-1/launch-week-day-1-cover.webp"/>
</head>

<div className='announcementContainer'>

<span class="badge badge--secondary">Launch Week 1.0</span>



<br></br>



# Feature in Spotlight: Logs Explorer [Day 1] 🪵

<div class="avatar">
  <a
    class="avatar__photo-link avatar__photo avatar__photo--lg"
    href="https://www.linkedin.com/in/ankit-anand-686a53a1/">
    <img
      alt="Ankit Profile"
      src="/img/users/ankit-anand.webp" />
  </a>
  <div class="avatar__intro">
    <div class="avatar__name">Ankit Anand</div>
    <small class="avatar__subtitle">
      Maintainer, SigNoz
    </small>
  </div>
</div>

<br />


Welcome to SigNoz Launch Week 1.0!

This is our first launch week, and we’re excited to introduce you to some cool new features in SigNoz. We ship fast but often miss sharing the story behind these features with our community.

Launch week for us is an opportunity to share the behind-the-scenes of new features that we have built in the recent past. Our open-source maintainers will share the story on the whats, whys, and hows of new upgrades to SigNoz!

<br></br>

<figure data-zoomable align='center'>
    <img className="box-shadowed-image" src="/img/events/launch-week-1/launch-week-day-1-cover.webp" alt="Launch week day 1 cover"/>
</figure>
<br/>


Every day of this week, we will be putting one feature in the spotlight and getting to know the story behind it. 

For day 1, the feature in the spotlight is the **Logs Explorer** in SigNoz. Out of the three signals of observability (metrics, traces, and logs), logs are the easiest one to start with for developers. While developing applications, developers use logs as the first signal to capture important information.

No wonder that it is one of the highest-used features in SigNoz. We have shipped a complete design revamp of Logs Explorer to enhance developer productivity.

<br></br>

## Builders - Nitya & Shuvam

[Nitya](https://www.linkedin.com/in/nityananda-gohain/) has built logs in SigNoz from the ground up. He was fascinated with the idea of an open-source observability tool and joined SigNoz early. Now Nitya is deep into logging with OpenTelemetry and taking logs at SigNoz to the next level.

[Shuvam](https://www.linkedin.com/in/shuvam-manna/) leads design at SigNoz. He fell in love with software products at an early age, and with a background in Computer Science, he is passionate about solving developer problems with design.

<figure data-zoomable align='center'>
    <img className="box-shadowed-image" src="/img/events/launch-week-1/logs-builder.webp" alt="Logs Explorer Builder"/>
</figure>

<br></br>

<br></br>

## Logs Explorer in SigNoz

Building a robust logs explorer has its own challenges. 

- **Different formats of logs:** Logs can be generated in any format, depending on the developer's preference or the system's requirements. This lack of standardization complicates the aggregation and analysis of logs.

- **Wide range of sources & deployment environments:** Logs can be produced by a wide range of sources. Applications can also be deployed in different environments like Docker, Kubernetes, bare metal, etc. Each environment might have its own method of log generation and transmission.

To build a generic logs explorer, you will need a system that understands logs in different formats from different sources and provides users with a way to query their logs. The flexibility that logs provide makes it difficult to analyze them properly.

SigNoz logs explorer is meant to overcome these challenges and provide developers with an easy way to collect and analyze their logs.

<br></br>

## Components of SigNoz Logs Explorer

### **Histogram**

Histogram shows the count of logs that were ingested in the specified time range. For example, in the below screenshot it shows the count of logs ingested in the last 30 minutes.

<figure data-zoomable align='center'>
    <img className="box-shadowed-image" src="/img/events/launch-week-1/histograms.webp" alt="Histogram in Logs Explorer"/>
    <figcaption><i>Histogram in Logs Explorer</i></figcaption>
</figure>
<br/>

### **Expanded View of Logs**

You can click on a log line to see the expanded view of the log. It shows the log body and all the attributes that are attached to it. The context view for a log shows other logs that were emitted before and after it by the same source. For example, the context view for a log emitted by a docker container will show it in context between the logs that were emitted before and after it by the same container. This can be useful for gaining more context while debugging issues.

<figure data-zoomable align='center'>
    <img className="box-shadowed-image" src="/img/events/launch-week-1/expanded-view-log-line.webp" alt="Expanded view of a log line"/>
    <figcaption><i>Expanded view of a log line</i></figcaption>
</figure>
<br/>



### **Filtering Options**

Searching through logs is the first thing a developer might want to do with logs. Our Logs Explorer has two ways to search and query your logs:

- **Search Filter:**<br></br>
    The search filter helps you query logs based on different attributes extracted.
    
    <figure data-zoomable align='center'>
    <img className="box-shadowed-image" src="/img/events/launch-week-1/search-filter.webp" alt="Search applied for `container_id=debian`"/>
    <figcaption><i>Search applied for `container_id=debian`</i></figcaption>
    </figure>
    <br/>
    
     
    
- **Advanced Query Builder:**<br></br>
    The advanced query builder helps you query logs and perform aggregation on it.

    <figure data-zoomable align='center'>
    <img className="box-shadowed-image" src="/img/events/launch-week-1/advanced-logs-query-builder.webp" alt="Advanced query builder"/>
    <figcaption><i>Applied `count` function on logs from `debian` container id</i></figcaption>
    </figure>
    <br/>
    


<br></br>

### Different Views in Logs Explorer

The logs explorer comes equipped with three different views:

- **List View:** 
It shows all your logs in a list. You can also configure this view to see log data in three different formats: raw, default, and columns, which come in handy to skim through your logs quickly.

- **Time Series:**
The time-series view shows charts for any aggregations that you perform on your logs using the advanced query builder. You can also add these views as panels to any dashboard.

- **Table:**
It shows the aggregated value for the specified time range.


<br></br>



## Features of SigNoz Logs Explorer

### Correlation of Logs to Traces

One of the greatest advantages of using SigNoz is the correlation of different signals. You can correlate your traces with logs that help in debugging performance issues quickly. 

In the flame graph view of traces, you can click on a particular span to check out its related logs. You need to ensure that your logs contain trace identifiers while instrumenting your application to use this feature.

<figure data-zoomable align='center'>
<img className="box-shadowed-image" src="/img/events/launch-week-1/logs-traces.webp" alt="Traced to logs"/>
<figcaption><i>Go to related logs for a particular span in a trace.</i></figcaption>
</figure>
<br/>

### Filtering JSON logs directly

If the body of your logs is in `JSON` format, you can directly filter your logs based on any attribute present in the `JSON` logs. This makes it very easy to create search filters from `json logs`.

<figure data-zoomable align='center'>
    <img className="box-shadowed-image" src="/img/events/launch-week-1/json-filter.gif" alt=""/>
    <figcaption><i></i></figcaption>
</figure>
<br/>

### Create Dashboards & Alerts

You can add any time-series chart that you create using the logs query builder to dashboards. You can either add it to an existing dashboard or create a new dashboard. The `Add to Dashboard` button can be seen at the bottom of the screen. This makes it very easy to monitor your logs in SigNoz.


<figure data-zoomable align='center'>
    <img className="box-shadowed-image" src="/img/events/launch-week-1/add-to-dashboard.gif" alt=""/>
    <figcaption><i></i></figcaption>
</figure>
<br/>



You will also get an option to `Create Alerts` directly from the logs explorer view. This makes it easy to create critical alerts from your logs data.

<figure data-zoomable align='center'>
<img className="box-shadowed-image" src="/img/events/launch-week-1/create-alerts.webp" alt="Traced to logs"/>
<figcaption><i>Create alerts from logs data directly from the Logs Explorer view</i></figcaption>
</figure>
<br/>


### Saved Views

You might apply multiple filters or write advanced queries on your log data. If you want to access logs pertaining to the same query, then you can use `Save this View` feature. Saving a view with the filters applied will let you access it easily whenever you need it in the future.

<figure data-zoomable align='center'>
<img className="box-shadowed-image" src="/img/events/launch-week-1/save-view.gif" alt="Traced to logs"/>
</figure>
<br/>


<br></br>


## OpenTelemetry’s Role in Logs Management

OpenTelemetry introduces a universal log model that defines a standard for log formats, including fields like timestamps, trace IDs, span IDs, resource attributes, and others. This standardization simplifies the process of collecting, processing, and analyzing logs from various sources and formats, making it easier for developers to implement and maintain observability practices.

You can also use the log model to map existing log formats to OpenTelemetry’s standard, which can help you standardize your log collection across your applications and hosts. Using OpenTelemetry, you can also correlate your logs with traces that can help developers troubleshoot issues more efficiently.


<br></br>


## Solving Search at Scale with ClickHouse

At SigNoz, we use ClickHouse for storing logs. ClickHouse is a very fast columnar database. Below are a few features of ClickHouse that we are using for improving search at scale.

1. **Materialized Views and Indexing:** ClickHouse allows for the creation of materialized views and indexing of extracted log attributes. This feature speeds up queries by pre-aggregating data and providing faster access to indexed data, thus solving the first problem of quickly filtering and finding relevant log lines.

2. **Handling High Cardinality Data:** ClickHouse excels at managing high cardinality data, such as unique trace IDs, efficiently. High cardinality fields can pose challenges in databases by requiring extensive resources to index and search. ClickHouse's capability to effectively handle such data ensures that searches over logs, even with high cardinality attributes, are performed swiftly and efficiently.

3. **Projections for Faster Searches(Upcoming):** Projections in ClickHouse allows data to be rearranged to optimize for specific types of queries. By creating projections based on common query patterns, such as filtering by service name, ClickHouse can provide quicker search results, making the analysis of logs more efficient.

<br></br>

## Design Considerations behind the New Logs Explorer

For a tool like SigNoz, which helps developers troubleshoot their applications, we optimize for developer productivity and not engagement. This is one of the key design philosophies behind revamping our Logs Explorer. 

Some of the key things that we solved with the revamp are:

- **Make data filtering more intuitive**<br></br>
    One of the key design goals was to make data filtering more intuitive. You will find the new design a lot more suited for querying your log data. For example, we have revamped the picker for time range selection to make it easier for users to filter logs over the required time range.

    <figure data-zoomable align='center'>
    <img className="box-shadowed-image" src="/img/events/launch-week-1/new-time-filter.webp" alt="Time picker"/>
    <figcaption><i>The new time picker lets you select your required time range easier with relative time section</i></figcaption>
    </figure>
    <br/>
    
    
    
- **Increasing Data Density Without Sacrificing Usability**<br></br>
    Recognizing the need for developers to view more log data at once, we aimed to make the interface more data-dense. However, we balanced this by ensuring that the added data did not overwhelm users or compromise the readability of logs.

    <figure data-zoomable align='center'>
    <img className="box-shadowed-image" src="/img/events/launch-week-1/logs-explorer-full.webp" alt="Increasing data density"/>
    <figcaption><i>One of the design goals was to enable developers to see as much log data at once as possible</i></figcaption>
    </figure>
    <br/>
    
    
    
- **Balancing Simplicity & Configurability**<br></br>
    The user base of SigNoz is diverse. One area we focused on was balancing simplicity for new users with the need for advanced configurations for power users. This led to bifurcating the logs query builder into a simple search bar and an advanced query builder.

    <figure data-zoomable align='center'>
    <img className="box-shadowed-image" src="/img/events/launch-week-1/search-and-query-builder.gif" alt="Traced to logs"/>
    </figure>
    <br/>
    

- **Simplifying Complex Information**<br></br>
    There is a lot of detail associated with a single log line which developers need to consume quickly. Our new design includes a side panel for log details, which you can access by clicking on a single log line. The side panel provides enough space to include a lot of details about log lines while also segregating views for things like seeing logs in context.

    <figure data-zoomable align='center'>
    <img className="box-shadowed-image" src="/img/events/launch-week-1/side-panel-logs.webp" alt="Logs Side Panel"/>
    <figcaption><i>The side panel for logs creates enough space to show all details related to a single log line in a consumable format</i></figcaption>
    </figure>



<br></br>


## Gathering Feedback for Design from Open-Source Community

One of the key advantages of SigNoz being an open-source project is that we can directly tap our open-source community for feedback. The first step for building any new feature is to go through issues opened by our open-source community. 

We don’t have to reach out to users for feedback, and there is a lot of inbound feedback, which serves as a valuable guide for us when creating new designs.


<br></br>



## What’s next?
    
On the design front, we will be working on revamping the way users interact with other signals in SigNoz, just like logs. A lot of design effort will also be on revamping the way users use dashboarding in SigNoz. Shuvam is working on pushing the boundaries of what shareable configurations can look like. We are also exploring ways to build on open standards for better compatibility with other tools. 

Nitya will be working on further advancing searching through logs at scale. Log data can be humungous and one of our key focus is to enable quick log search at any scale. On that front, Nitya will be exploring projections in ClickHouse more deeply.


<p>&nbsp;</p>

<LiteYoutubeEmbed id="4_uVfiNB4oY" mute={false} />

<p>&nbsp;</p>


# Features in Spotlight:

<br></br>

<div class="row spotlight-row">
  <div class="col col--6">
    <div class="card-demo">
      <a class="card" href="https://signoz.io/newsroom/launch-week-1-day-1/"
						rel="noopener noreferrer"
						target="_blank">
        <div class="card__image">
        <img
          src="/img/events/launch-week-1/launch-week-day-1-cover.webp"
          alt="Image alt text"
          title="Launch Week Day 1" />
        </div>
        <div class="card__body">
        <h4>Feature in Spotlight: Logs Explorer</h4>
        <small>
          Builder: Nitya & Shuvam.
        </small>
        </div>
      </a>
    </div>
  </div>

  <div class="col col--6">
    <div class="card-demo">
      <div class="card">
        <div class="card__image">
        <img
          src="/img/events/launch-week-1/signoz-launch-week-coming-soon.webp"
          alt="Image alt text"
          title="Launch Week Day 2" />
        </div>
        <div class="card__body">
        <h4>Feature in Spotlight: Day 2</h4>
        <small>
          Coming Soon...
        </small>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="row spotlight-row">
<div class="col col--6">
<div class="card-demo">
  <div class="card">
    <div class="card__image">
      <img
        src="/img/events/launch-week-1/signoz-launch-week-coming-soon.webp"
        alt="Image alt text"
        title="Launch Week Day 3" />
    </div>
    <div class="card__body">
      <h4>Feature in Spotlight: Day 3</h4>
      <small>
        Coming Soon...
      </small>
    </div>
    
  </div>
</div>
</div>

<div class="col col--6">
<div class="card-demo">
  <div class="card">
    <div class="card__image">
      <img
        src="/img/events/launch-week-1/signoz-launch-week-coming-soon.webp"
        alt="Image alt text"
        title="Launch Week Day 4" />
    </div>
    <div class="card__body">
      <h4>Feature in Spotlight: Day 4</h4>
      <small>
        Coming Soon...
      </small>
    </div>

  </div>
</div>
</div>
</div>

<div class="row spotlight-row">

<div class="col col--6">
<div class="card-demo">
  <div class="card">
    <div class="card__image">
      <img
        src="/img/events/launch-week-1/signoz-launch-week-coming-soon.webp"
        alt="Image alt text"
        title="Launch Week Day 5" />
    </div>
    <div class="card__body">
      <h4>Feature in Spotlight: Day 5</h4>
      <small>
        Coming Soon...
      </small>
    </div>
    
  </div>
</div>
</div>
</div>


</div>