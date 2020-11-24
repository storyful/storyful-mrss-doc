# Storyful MRSS Guide for External Use

## What does Storyful provide through MRSS?

Storyful stories can belong to one or more Channels. Storyful can provide any published story in a channel in the CMS through MRSS. The system works by channel and an MRSS feed can include multiple channels. e.g. Video Partners, or even World News, Weather, and Viral.
What goes in a channel is controlled by our journalists. There are some rules we can configure on the MRSS feed to filter out certain stories. However the configured channels for an MRSS feed largely set the tone of the MRSS feed.
Each story has a Clearance state associated with it. Clearance dictates what the client can do with the content linked to the Story.

## FAQ

### How many stories in each MRSS feed?

The 50 latest stories.

### Can the archive be supplied via MRSS?

Yes, the feed has a special backfill mode that allows playback of historical content. See below for details.

### What data is in the MRSS?

The most relevant information supplied in the MRSS include the title, summary, credit, and MP4 of a story. The full list of information is in the Storyful Video - Technical section below.

### Can we provide XYZ video format?

Storyful does not alter the original format of the asset provided. In most cases that format is MP4.

### Do all stories have an MP4 file?

Most but not all, and even fewer if World News or Weather channels are provided. The Video Partners channel is meant to guarantee MP4 files but this is up to the journalist and there is no technical check.

### Can we delay delivery of published stories?

Yes, a published story can be delayed per MRSS feed by up to 120 minutes.

### How quickly will a partner get a story through MRSS?

This depends how often they poll the URL and if there is any delay on their MRSS feed. If they time it right they can get the story instantly. We do not provide guidance on being “instant” though.

### How often can a partner poll?

As often as they want. We have one partner who polls every minute. We recommend every 5 minutes as more frequent polling will gain little.

### What about Trends stories?

Stories in the Trends channel tend not to work well in MRSS. Our MRSS favours the style of story written for World News, Weather, Viral and Video Partners. These are stories with a primary piece of content; a video, a title, and a summary. Technically a Trends story with a primary piece of content, the MP4 set etc. will work fine in MRSS. The partner will not get all the other pieces of content in the Trends story though.

### What about “Full rss”?

Technically we can supply the entire story via MRSS. But we’ve found in practice that it is unwieldy for partners and too specific to how Storyful displays stories. We do not recommend “Full rss” feeds.

### Are there categories or keywords?

Yes, both. Certain partners have custom categories which are selected by the journalist and are present in the feed. All other partners get the standard categories by default. Keywords entered by a journalist are available in the MRSS. IPTC Categories, recently added to Storyful stories via the CMS, can now be returned. Inclusion of the IPTC categories for stories can be enabled on the feed via the feed configuration page within admin.

### Can we filter on profanity, nudity, violence, and other guidance?

Yes, stories have a GUIDANCE field set by the journalists which MRSS can filter on.

### How do we get transcriptions (captions) for videos?

Contact support@storyful.com to have transcriptions enabled for your MRSS feed.

Not all the videos in our feeds will have the `<media:text>` XML elements transcriptions.
Transcriptions are automatically generated using machine learning but may not be available in cases
where there is no speech present, speech is too short or unclear because of multiple speakers or background noise. Jargon or slang can also reduce the accuracy of the transcription.

### Does Storyful host the video files?

Technically Storyful does host the original video files but we ask that our partners download the video files, ingest them into their content systems, and serve the video from their system. This is because Storyful does not want to incur the costs or complexity of serving video for hundreds of millions of views.

## Storyful Video - Technical

Storyful typically provides original video files from a variety of platforms including but not restricted to YouTube, Facebook, and Instagram.

### Delivery

Storyful delivers video metadata as MRSS or via a custom API available in XML or JSON.

### MRSS

The MRSS provides up to 50 items at a time in reverse chronological order with the following key metadata. Note that Storyful produces stories which for MRSS purposes contain at most one video reference:

*   title of story written by Storyful staff.
*   description and summary of story.
*   image with url, title and link.
*   pubDate and originalPubDate of item to the MRSS.
*   link back to the story on Storyful.com.
*   guid of the MRSS item.
*   author is the owner of the video in the story.
*   storyful:clearance is the title and description as entered by the author for the clearance status of the story.
*   storyful:guidance is the title and description as entered by the author for the guidance advice for the story.
*   storyful:slug is the slug of the story e.g. MEXICO.
*   storyful:channels is the list of channels the story is assigned to.
*   storyful:categories is the list of Storyful Newswire categories (News, Politics, Funny etc.) that the story is assigned to.
*   media:title is the title of the story written by Storyful staff.
*   media:description is the description and summary of story.
*   media:credit required credit text as written by Storyful staff.
*   media:content with url to the video file and the lang (typically en) of the video file. Where the video duration is known, we populate the optional duration attribute (in seconds).
*   media:keywords as written by Storyful staff.
*   media:category as chosen by Storyful staff.
*   media:text provides an audio transcription of the video with start and end time offsets.
*   media:thumbnail with the url of a key frame from the video. Items may have more than one thumbnail reference with alternative sizes and crops. The width and height of thumbnails are included as attributes, if known.

* There are also several Ooyala elements which are temporary and should not be relied on.
* The category elements usually contain keywords that our journalists associate with each piece of content. However, if required, a feed can by configured to use IPTC categories in these elements instead. The ‘scheme’ attribute is only present when IPTC categories are enabled on the feed.

### Sample
```
<rss xmlns:content="http://purl.org/rss/1.0/modules/content/" xmlns:media="http://search.yahoo.com/mrss/" xmlns:atom="http://www.w3.org/2005/Atom" xmlns:storyful="http://storyful.com/mrss" xmlns:ooyala="http://www.ooyala.com/mrss/" version="2.0">
  <channel>
    <title>Storyful</title>
    <description>
      Storyful.com is a place to share stories with people who want to listen.
    </description>
    <link>
      https://mrss.storyful.com/v2/123456789.xml
    </link>
    <atom:link href="https://storyful.com/rss/123456789.xml" rel="self" type="application/rss+xml"/>
    <lastBuildDate>Thu, 06 Oct 2016 01:04:34 +0000</lastBuildDate>
    <item>
      <title>
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce mollis id libero ac posuere.
      </title>
      <description>
      <![CDATA[
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce mollis id libero ac posuere. Suspendisse at metus tempus nulla auctor consectetur nec non arcu. Quisque nec scelerisque purus. Maecenas sed metus nec lacus malesuada faucibus eu ac sem. Morbi pellentesque, libero sed semper volutpat, libero dui congue nulla, vel sollicitudin nisl sapien id nisi. Duis sit amet luctus elit, ac hendrerit tellus. </p>
        ]]>
      </description>
      <guid>https://storyful.com/stories/123</guid>
      <link>https://storyful.com/stories/123</link>
      <pubDate>Thu, 15 Dec 2016 09:24:07 +0000</pubDate>
      <author>Name &lt;email.address&gt;</author>
      <category scheme="https://www.iptc.org/std/photometadata/documentation/GenericGuidelines/index.htm">disaster and accident</category>
      <summary>
        <![CDATA[
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce mollis id libero ac posuere. Suspendisse at metus tempus nulla auctor consectetur nec non arcu. Quisque nec scelerisque purus. Maecenas sed metus nec lacus malesuada faucibus eu ac sem. Morbi pellentesque, libero sed semper volutpat, libero dui congue nulla, vel sollicitudin nisl sapien id nisi. Duis sit amet luctus elit, ac hendrerit tellus. </p>
        ]]>
      </summary>
      <image>
        <url>
          https://storyful.s3.amazonaws.com/production/stories/000.png
        </url>
        <title>From: Author</title>
        <link>
          https://www.facebook.com/
        </link>
      </image>
      <originalPubDate>Thu, 15 Dec 2016 09:24:07 +0000</originalPubDate>
      <storyful:clearance title="CLEARED">
        <![CDATA[
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce mollis id libero ac posuere. </p>
        ]]>
      </storyful:clearance>
      <storyful:slug>SPACE</storyful:slug>
      <storyful:channels>
        <storyful:channel slug="">Channel MRSS</storyful:channel>
      </storyful:channels>
      <storyful:categories>
        <storyful:category>politics</storyful:category>
        <storyful:category>human interest</storyful:category>
      </storyful:categories>
      <media:title>
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce mollis id libero ac posuere.
      </media:title>
      <media:description type="html">
        <![CDATA[
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce mollis id libero ac posuere. Suspendisse at metus tempus nulla auctor consectetur nec non arcu. Quisque nec scelerisque purus. Maecenas sed metus nec lacus malesuada faucibus eu ac sem. Morbi pellentesque, libero sed semper volutpat, libero dui congue nulla, vel sollicitudin nisl sapien id nisi. Duis sit amet luctus elit, ac hendrerit tellus. </p>
        ]]>
      </media:description>
      <media:credit>Facebook</media:credit>
      <media:content url="https://storyful.s3.amazonaws.com/video/syfl-067aba5e2994a21fc3a0a26d112cd957.mp4" medium="video" lang="en" duration="60"/>
      <media:keywords>School bus, Portland-Oregon, Facebook</media:keywords>
      <media:category>News</media:category>
      <media:thumbnail url="https://storyful.s3.amazonaws.com/production/stories/000.PNG" medium="image" />
      <media:thumbnail url="https://storyful.s3.amazonaws.com/production/stories/001.PNG" medium="image" width="1028" height="720" />
      <media:text type="plain" lang="en-US" start="00:00:03.25" end="00:00:03.46">Lorem</media:text>
      <media:text type="plain" lang="en-US" start="00:00:04.100" end="00:00:05.45">Ipsum</media:text>
      <media:text type="plain" lang="en-US" start="00:00:08.59" end="00:00:11.54">Consectetur adipiscing.</media:text>
      <media:text type="plain" lang="en-US" start="00:00:12.65" end="00:00:12.97">Duis sit amet luctus elit, ac hendrerit tellus.</media:text>
      <ooyala:metadata name="summary">
        <![CDATA[
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce mollis id libero ac posuere. Suspendisse at metus tempus nulla auctor consectetur nec non arcu. Quisque nec scelerisque purus. Maecenas sed metus nec lacus malesuada faucibus eu ac sem. Morbi pellentesque, libero sed semper volutpat, libero dui congue nulla, vel sollicitudin nisl sapien id nisi. Duis sit amet luctus elit, ac hendrerit tellus. </p>
        ]]>
      </ooyala:metadata>
      <ooyala:metadata name="originalPubDate">Thu, 15 Dec 2016 09:24:07 +0000</ooyala:metadata>
      <ooyala:metadata name="pubDate">Thu, 15 Dec 2016 09:24:07 +0000</ooyala:metadata>
      <ooyala:metadata name="author">Name &lt;email.address&gt;</ooyala:metadata>
      <ooyala:labels>/Home/Telegraph TV,/Sources/Storyful</ooyala:labels>
    </item>
  </channel>
</rss>
```

### Formats

Storyful provides video files in the following formats:

Ref# | Container | Resolution | Video Encoding | Video Bitrate(Mbit/s) | Audio Encoding | Audio Bitrate(kbit/s)
-----|-----------|------------|----------------|-----------------------|----------------|----------------------
1 | MP4 | 270p | H.264 | 0.5 | AAC | 96
2 | MP4 | 360p | H.264 | 0.5 | AAC | 96
3 | MP4 | 720p | H.264 | 2-2.9 | AAC | 192
4 | MOV | 720p | MJPEG | 15.87 | AAC | 192

1, 2 and 3 are dependant on the originating platform. We do not transcode or provide multiple options in these cases. The only option is 4 where we transcode by special request.

### Ratios/Formats and Letterboxing

Storyful provides video files with the following ratios and letterboxing options:

Ref# | Provided Ratio/Format | Letterboxing
-----|-----------------------|-------------
1 | From Origin | From Origin
2 | From Origin | From Origin
3 | From Origin | From Origin
4 | 16:9 | Yes (if needed)

1.  “From Origin” means that Storyful does not process the video file ratio/format or add/remove letterboxing. The ratio/format and letterboxing is provided as-is from the originating platform.
2.  Because in some cases Storyful provides the original file from the originating platform you may get:
    *   Landscape format with letterboxing top and bottom.
    *   Landscape format without letterboxing.
    *   Portrait format with letterboxing left and right.
    *   Portrait format without letterboxing.
3.  Storyful have seen very tall and narrow videos from Facebook and very short and wide videos from YouTube. Instagram is typically 1:1 but not always.
4.  Storyful ensures videos are provided in the correct orientation.

## Authentication

Contact support@storyful.com for your permanent access token.

## Base

`https://mrss.storyful.com/v2/<acess_token>.xml`

## Version

The current version of the Storyful MRSS is 2

## XML

The default response type is XML.

## Optional Query String Parameters

The following optional parameters can be included and combined in the query string. If a parameter is not explicitly included, or is blank, then the default value is assumed.

name | type | description | default value | example
-----|------|-------------|---------------|--------
items | integer | Number of items (stories) returned. | 50 | items=10
brief | boolean | Use shorter content for summary and description elements. | n | brief=y
html | boolean | Allow HTML tags in summary and description elements. | y | html=n
bare| boolean | It removes clearance mark from story titles. | y | bare=n
strict | boolean | It includes only standard nodes. | n | strict=y
thumbs | boolean | Include media thumbnail elements. | y | thumbs=n 

## Filters
The following optional parameters can be included in the query string to allow you to narrow results.
NOTE: Multiple filters are not currently supported.

name | description | example
-----|-------------|--------
ids | filter results by specific identifier | ?ids=165220 or ?ids=165225,165220
channel | filter results by channel | ?channel=licensed
collection | filter results by collection | ?collection=venezuela-antigovernment-protests_2937
slug | filter results by slug | ?slug=US-PA
keywords | filter results by the contents of the media:keywords element. Multiple keywords in the filter are treated as a boolean OR. Keywords are case-insensitive | ?keywords=pet or ?keywords=pet,cat,dog
categories | filter results by Storyful Newswire category. Multiple categories in the filter are treated as a boolean OR. Categories are case-insensitive. Spaces in category names should be replaced with hyphens '-'. | ?categories=news or ?categories=news,weather-and-science

## Backfill support

Our feeds support a temporary mode that allows for bulk backfilling of our content archive. While in this mode, each poll of the feed will return a batch of stories from
the archive, starting with the oldest stories first.  Once all stories have been returned in this way, the feed reverts to normal mode. If you require an initial backfill of content as part of your feed configuration then please contact our support team.

## Support

Contact support@storyful.com with any questions or issues.
