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
  - User publish 5 comments per day
  ### 🔹 5. Limits
   - User can publish max 10 photos per post
   - Max size of photo 500KB
 ### 🔹 6. Timings
  - Create post, comment posts, like posts <= 1s
  - Upload photos, search posts, load feeds <= 3s

## 📈 Estimated System Load Analysis
 
