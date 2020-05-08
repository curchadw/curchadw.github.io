---
layout: post
title:      "My Minority Biz Gem CLI"
date:       2020-05-08 02:55:44 +0000
permalink:  my_minority_biz_gem_cli
---


I was in a previous bootcamp and this one by far has pushed me beyond some of my limits, and I am not even past my first module yet...well I will be pretty soon. This projet has helped me reinforced some of the the things I've learned. With the help of my cohort lead and others, I am thinkful. I was pretty scared at first but relieved that I am alost finished.

What is my project about? My gem is is small directory of primarily black owned or ran businesses in San Antonio. I used the technique of scraping for this project since there was no available api  for fo the website in particular. I had no choice but to scrape four different pages since the url were routed differently.


```
require 'nokogiri'
require 'open-uri'
require 'pry'
require_relative '../minority_biz/business.rb'


class Scraper

 def self.scrape_first_page
        
        html = open("https://www.texasblackpages.com/united-states/san-antonio")
        doc = Nokogiri::HTML(html)
        doc.css('div.grid_element').each do |business|    
            biz = Business.new
            biz.name = business.css('a b').text
            biz.type = business.css('span.hidden-xs').text
            biz.number = business.css('span.sm-block.lmargin.sm-nomargin').text.gsub("\r\n","").strip
            
            
        end 
        
    end
		
		end
```

It also involved moderate usge of object oreinted programming and mass assignments to help create hash objects, which seemed different in convention compared to some other languages, but the concept is still the same. That's my own opinion by the way


```
class Business
    
    @@all = Array.new
    

    attr_accessor :name, :type, :number
    

    def initialize(attributes = nil)
        if attributes
        attributes.each {|key,value| self.send(("#{key}="),value)}
        end
        @@all << self
        
    end

```


I had issues piecing some of this together only because I was not cofortable with it, but with more practice it will come second nature. This project helped me get more familiar with using version control with github, and how to integrate existing gems or other project to your repos. y repos will only get bigger from here.








