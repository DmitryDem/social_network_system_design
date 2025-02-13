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
  - User publish 15 comments per day
  - User attach 10 photos to post
  - User likes 10 posts per day
  ### 🔹 5. Limits
   - Max size of photo up to 800KB
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

    Row size = 2472 bytes
  - Comments
    
    | Column Name  | Data Type     | Description                              |  Size (bytes)|
    |--------------|---------------|------------------------------------------|--------------|
    | Id           | INT           | Unique identifier for the comment        |  4           |
    | UserId       | INT           | References the user who comment          |  4           |
    | Comment      | NVARCHAR(2048)| Comment content                          |  1024        |
    | ParentId     | INT           | Parent comment (if comment is reply)     |  4           |
    | PostId       | INT           | Post Id                                  |  4           |

    Row size = 1040 bytes

    - Reactions
      
    | Column Name  | Data Type     | Description                              |  Size (bytes)|
    |--------------|---------------|------------------------------------------|--------------|
    | UserId       | INT           | References the user who like/unlike      |  4           |
    | PostId       | INT           | Post Id  4                               |  4           |
    | Like         | BIT           | Like/Unlike                              |  1           |

     Row size = 9 bytes

    ### 🔹 Calculation 
