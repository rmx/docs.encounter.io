---
title: API - Events
---

# Alphabetical list of all events

<% Dir['content/api/event/*'].sort {|a,b|
    if a.downcase == b.downcase
        a <=> b
    else
        a.downcase <=> b.downcase
    end
}.each do |x| %>
<% name = x.gsub(/content.api.event./, '').gsub(/.md$/, '') %>
<%= "- [#{name}](/api/event/#{name}/)" %>
<% end %>
