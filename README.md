# social_network_system_design

## 🚀 Functional Requirements

### 🔹 1. Users can **publish travel posts** with
  - Photos (**JPEG, PNG).
  - Description
  - Geolocation
 
 ### 🔹 2. Users can like posts others travellers
 ### 🔹 3. Users can comments posts others travellers
 ### 🔹 4. Users can follow travelers and notify about their updates.
 ### 🔹 5. Users can search for popular travel destinations and view posts from those places;
 ### 🔹 6. Users can view other travelers feeds and the user's feed based on follows in reverse chronological order;

---
 ## 📊 Non-Functional Requirements
  ### 🔹 1. 10 000 000 DAU
  ### 🔹 2. 99.95% uptime target.
  ### 🔹 3. Posts, photos and comments are always stored
  ### 🔹 4. Users activity (average)
  - User publish 3 posts per week.
  - User view 20 posts per day
  - User add 5 comments per day
  - User view 20 comments per post
  - User view 10 likes per post
  - Post contains 150 comments per day
  - Post contains 800 likes per day
  - User publish 10 photos per post
  - User likes 10 posts per day
  ### 🔹 5. Limits
   - Max size of photo up to 800KB
   - Using paging for
     - posts  - 10 per page
     - comments - 10 per page
     - likes - 20  per page
 ### 🔹 6. Timings
  - Create post, comment posts, like posts <= 1s
  - Upload photos, search posts, load feeds <= 3s

## 📈 Estimated System Load Analysis
  ### 🔹 Data    
  - Posts
    
    | Column Name  | Data Type     | Description                              |  Size (bytes)|
    |--------------|---------------|------------------------------------------|--------------|
    | Id           | INT           | Unique identifier for the post           |  4           |
    | UserId       | INT           | References the user who created the post |  4           |
    | Description  | NVARCHAR(1024)| Main content of the post                 |  2048        |
    | Country      | NVARCHAR(100) | Country where the post is related to     |  200         |
    | City         | NVARCHAR(100) | City where the post was made             |  200         |
    | Location     | GEOGRAPHY     | Geographic location (latitude, longitude)|  16          |

    Row size = 2472 bytes = 2.472 KB
  - Comments
    
    | Column Name  | Data Type     | Description                              |  Size (bytes)|
    |--------------|---------------|------------------------------------------|--------------|
    | Id           | INT           | Unique identifier for the comment        |  4           |
    | UserId       | INT           | References the user who comment          |  4           |
    | Comment      | NVARCHAR(2048)| Comment content                          |  1024        |
    | ParentId     | INT           | Parent comment (if comment is reply)     |  4           |
    | PostId       | INT           | Post Id                                  |  4           |

    Row size = 1040 bytes = 1.040 KB

    - Reactions
      
    | Column Name  | Data Type     | Description                              |  Size (bytes)|
    |--------------|---------------|------------------------------------------|--------------|
    | UserId       | INT           | References the user who like/unlike      |  4           |
    | PostId       | INT           | Post Id  4                               |  4           |
    | Like         | BIT           | Like/Unlike                              |  1           |

     Row size = 9 bytes = 0.009 KB

    ### 🔹 Calculation
    
    RPS (Write) = (10 000 000 (DAU) * ((3/7)(posts) * 10 (photos per post)) + 10(comments) + 10(likes))) / 86400 = 2810
    
    RPS (Read) = (10 000 000 (DAU) * (10 (posts) * 2 (pages) * 10 (photos) + 10 (comments) * 2 (pages) + 1 (likes)) / 86400) = 25578

    Network Traffic (Write) = (10 000 000 (DAU) * (3/7)(posts per day) * 2.472(post size) * 10(photos) * 800(photo size) + 10(comments) * 1.040(comment size) + 10 (likes) * 0.009(like size)) / 86400 = 982 MB/s
    
    Network Traffic (Read) = (10 000 000 (DAU) * 20(posts) * 2.472(post size) * 10(photos) * 800(photo size) + 20(comments) * 1.040(comment size) + 20 (likes) * 0.009(like size)) / 86400 = 4.58 GB/s
