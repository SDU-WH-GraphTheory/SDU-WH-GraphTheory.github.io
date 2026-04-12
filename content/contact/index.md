---
title: Contact
#date: 2022-10-24

type: landing

sections:
  - block: contact
    content:
      title: 联系我们
      text: |-
        若您对本课题组的研究方向、科研成果、合作交流或人才培养等方面感兴趣，欢迎通过以下方式与我们取得联系。我们期待与国内外同行及有志于学术研究的同学进行沟通交流、探讨合作，共同推动相关领域的科研与发展。
      email: hmsong@sdu.edu.cn
      phone: 0631-5688523
      address:
        street: 怡园街道
        city: 威海
        region: CA
        postcode: '94305'
        country: 中华人民共和国
        country_code: CN
      coordinates:
        latitude: '37.4275'
        longitude: '-122.1697'
      directions: 山东省威海市文化西路180号 山东大学 数学与统计学院
      office_hours:
        - '周五 14:00 to 17:00'
      appointment_url: 'https://calendly.com'
      #contact_links:
      #  - icon: comments
      #    icon_pack: fas
      #    name: Discuss on Forum
      #    link: 'https://discourse.gohugo.io'
    
      # Automatically link email and phone or display as text?
      autolink: true
    
      # Email form provider
      form:
        provider: netlify
        formspree:
          id:
        netlify:
          # Enable CAPTCHA challenge to reduce spam?
          captcha: false
    design:
      columns: '1'

  - block: markdown
    content:
      title:
      subtitle: ''
      text:
    design:
      columns: '1'
      background:
        image: 
          filename: contact.jpg
          filters:
            brightness: 1
          parallax: false
          position: center
          size: cover
          text_color_light: true
      spacing:
        padding: ['20px', '0', '20px', '0']
      css_class: fullscreen
---
