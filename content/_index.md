---
# Leave the homepage title empty to use the site title
title: Home
date: 2022-10-24
type: landing

sections:
  - block: about.biography
    id: about
    content:
      title: Biography
      # Choose a user profile to display (a folder name within `content/authors/`)
      username: admin
  - block: collection
    id: featured
    content:
      title: Featured
      filters:
        folders:
          - post
          - publication
        featured_only: true
    design:
      columns: '2'
      view: card
  - block: collection
    id: publications
    content:
      count: 2
      title: Recent Publications
      # text: |-
      #   {{% callout note %}}
      #   Quickly discover relevant content by [filtering publications](./publication/).
      #   {{% /callout %}}
      filters:
        folders:
          - publication
        exclude_featured: false
    design:
      columns: '2'
      view: citation
  - block: collection
    id: posts
    content:
      title: Recent Blogs
      subtitle: ''
      text: ''
      # Choose how many pages you would like to display (0 = all pages)
      count: 3
      # Filter on criteria
      filters:
        folders:
          - post
        # author: ""
        category: "DONE"
        # tag: ""
        exclude_featured: false
        exclude_future: false
        exclude_past: false
        publication_type: ""
      # Choose how many pages you would like to offset by
      offset: 0
      # Page order: descending (desc) or ascending (asc) date.
      order: desc
    design:
      view: compact
      columns: '2'
  # - block: portfolio
  #   id: projects
  #   content:
  #     title: Projects
  #     filters:
  #       folders:
  #         - project
      # Default filter index (e.g. 0 corresponds to the first `filter_button` instance below).
      # default_button_index: 0
      # Filter toolbar (optional).
      # Add or remove as many filters (`filter_button` instances) as you like.
      # To show all items, set `tag` to "*".
      # To filter by a specific tag, set `tag` to an existing tag name.
      # To remove the toolbar, delete the entire `filter_button` block.
      # buttons:
      #   - name: All
      #     tag: '*'
      #   - name: Deep Learning
      #     tag: Deep Learning
      #   - name: Other
      #     tag: Demo
    # design:
    #   # Choose how many columns the section has. Valid values: '1' or '2'.
    #   columns: '1'
    #   view: showcase
    #   # For Showcase view, flip alternate rows?
    #   flip_alt_rows: false
  - block: contact
    id: contact
    content:
      title: Contact
      # subtitle:
      # text: |-
      #   Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam mi diam, venenatis ut magna et, vehicula efficitur enim.
      # Contact (add or remove contact options as necessary)
      email: tangxiangong@gmail.com
      # phone: 888 888 88 88
      # appointment_url: ''
      # address:
      #   street: 450 Serra Mall
      #   city: Stanford
      #   region: CA
      #   postcode: '94305'
      #   country: United States
      #   country_code: US
      # directions: Enter Building 1 and take the stairs to Office 200 on Floor 2
      # office_hours:
      #   - 'Monday 10:00 to 13:00'
      #   - 'Wednesday 09:00 to 10:00'
      # contact_links:
      #   - icon: youtube
      #     icon_pack: fab
      #     name: Notion 
      #     link: 'https://xiaoxiaoyu.notion.site'
      #   - icon: blog
      #     icon_pack: fab
      #     name: FlowUs 
      #     link: 'https://xiaoxiaoyu.flowus.cn'
      #   - icon: twitter
      #     icon_pack: fab
      #     name: DM Me
      #     link: 'https://twitter.com/Twitter'
      #   - icon: skype
      #     icon_pack: fab
      #     name: Skype Me
      #     link: 'skype:echo123?call'
      #   - icon: video
      #     icon_pack: fas
      #     name: Zoom Me
      #     link: 'https://zoom.com'
      # Automatically link email and phone or display as text?
      autolink: true
      # Email form provider
      # form:
      #   provider: netlify
      #   formspree:
      #     id:
      #   netlify:
      #     # Enable CAPTCHA challenge to reduce spam?
      #     captcha: false
    design:
      columns: '2'
---
