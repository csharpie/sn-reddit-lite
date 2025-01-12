# Reddit Lite

An application used strictly to practice for the CAD (Certified Application Developer) Exam.

**Disclaimer**: _The application is intended strictly for personal use ONLY._

## Purpose

Allow users to create their own Subreddits inside of ServiceNow of which they subscribe, they can create posts, they comment on posts, and they can up-vote/down-vote posts. Reddit Lite Subreddits can be seeded with posts from Reddit.com as well.

## Business Requirements

### Tables

- Subreddit
  - New table
  - Fields
    - started_by
      - Reference (sys_user)
    - started
      - Date Time
    - name
      - String (50 characters)
    - banned_users
      - List (sys_user)
    - moderator_users
      - List (sys_user)
- Post
  - New table extended from task
  - Fields
    - subreddit
      - Reference (subreddit)
    - title
      - String (100 characters)
    - description
      - String (Max characters)
    - original_author
      - String (50 characters)
    - is_removed
      - True/False
    - ups
      - Integer
    - downs
      - Integer
    - score
      - Integer

### Personas

- User
  - Can read all posts
  - Can create any post
  - Can write own posts
  - Can delete own posts
- Admin
  - Can read all posts
  - Can create any post
  - Can write all posts
  - Can delete all posts
  - Can write post.is_removed of all subreddits
  - Can write subreddit.banned_users of all subreddits
  - Can write subreddit.moderator_users of all subreddits
- Moderator
  - Can read all posts of subreddits they moderate
  - Can delete all posts of subreddits they moderate
  - Can write post.is_removed of subreddits they moderate
  - Can write subreddit.banned_users of subreddits they moderate

### Flow

- Banned from subreddit
  - Sends notification to user when they are banned by an admin or moderator

### Data Source
- Subreddit (Hot 5 Posts)
  - Source file 
    - https://www.reddit.com/${SUBREDDIT}/hot.json?limit=4
 - Fields
    - children
      - data
        - title
        - selftext
        - id
        - author_fullname
        - ups
        - downs
        - score
