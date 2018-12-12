# [Design Twitter](https://leetcode.com/problems/design-twitter/description/)

Design a simplified version of Twitter where users can post tweets, follow/unfollow another user and is able to see the 10 most recent tweets in the user's news feed. Your design should support the following methods:

1. **postTweet\(userId, tweetId\)**: Compose a new tweet.
2. **getNewsFeed\(userId\)**: Retrieve the 10 most recent tweet ids in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user herself. Tweets must be ordered from most recent to least recent.
3. **follow\(followerId, followeeId\)**: Follower follows a followee.
4. **unfollow\(followerId, followeeId\)**: Follower unfollows a followee.

### **Example**

```
Twitter twitter = new Twitter();

// User 1 posts a new tweet (id = 5).
twitter.postTweet(1, 5);

// User 1's news feed should return a list with 1 tweet id -> [5].
twitter.getNewsFeed(1);

// User 1 follows user 2.
twitter.follow(1, 2);

// User 2 posts a new tweet (id = 6).
twitter.postTweet(2, 6);

// User 1's news feed should return a list with 2 tweet ids -> [6, 5].
// Tweet id 6 should precede tweet id 5 because it is posted after tweet id 5.
twitter.getNewsFeed(1);

// User 1 unfollows user 2.
twitter.unfollow(1, 2);

// User 1's news feed should return a list with 1 tweet id -> [5],
// since user 1 is no longer following user 2.
twitter.getNewsFeed(1);
```

### Note

一个典型的 Observer pattern；为了降低耦合度，每个 user 维护自己的 tweet list 和 follow list，而 post tweet 只是负责自行生产，而不主动执行 push; 每次刷新的时候自己从 follow 列表抓 tweets 就好了。

这题一个需要注意的细节是，排序顺序是按照 timestamp，接口里给的 tweetId ，和时间顺序没有必然的联系，所以要自行维护全局时间戳。

除此之外就是比较直观的 merge k sorted list 问题了，为了方便处理，我们维护了一个 Tweet object 的 LinkedList，但同时 Tweet 存了一个自己的 prev 指针，方便进行多路归并的时候正确找到下一个元素。

其他需要注意的就是各种 corner case : 关注自己，取关不存在的人，取关自己本来就没关注的人，自己或者自己的关注用户没有任何 post，等等

### Code

```java
class Twitter {

    // Key : user
    // Value : list of tweets
    Map<Integer, LinkedList<Tweet>> tweetsMap;
    // Key : user
    // Value : list of userId's the user has been following
    Map<Integer, Set<Integer>> follows;
    
    int timestamp;
    /** Initialize your data structure here. */
    
    private class Tweet implements Comparable<Tweet> {
        int timestamp;
        int tweetId;
        Tweet prev;

        public Tweet(int timestamp, int tweetId, Tweet prev) {
            this.timestamp = timestamp;
            this.tweetId = tweetId;
            this.prev = prev;
        }
        public int compareTo(Tweet a) {
            return a.timestamp - this.timestamp;
        }
    }
    
    public Twitter() {
        tweetsMap = new HashMap<Integer, LinkedList<Tweet>>();
        follows = new HashMap<Integer, Set<Integer>>();
        timestamp = 0;
    }
    
    /** Compose a new tweet. */
    public void postTweet(int userId, int tweetId) {
        if (!tweetsMap.containsKey(userId)) {
            tweetsMap.put(userId, new LinkedList<Tweet>());
        }
        Tweet prev = (tweetsMap.get(userId).size() == 0) ? null: tweetsMap.get(userId).peekFirst();
        tweetsMap.get(userId).offerFirst(new Tweet(timestamp, tweetId, prev));
        timestamp++;
    }
            
    /** 
    Retrieve the 10 most recent tweet ids in the user's news feed. 
    Each item in the news feed must be posted by users who the user followed or by the user herself. 
    Tweets must be ordered from most recent to least recent. 
    */
    public List<Integer> getNewsFeed(int userId) {
        List<Integer> list = new ArrayList<>();
        PriorityQueue<Tweet> maxHeap = new PriorityQueue<Tweet>();

        if (tweetsMap.containsKey(userId) && 
            tweetsMap.get(userId).size() > 0) {
            maxHeap.offer(tweetsMap.get(userId).peekFirst());
        }

        if (follows.containsKey(userId)) {
            for (int followee : follows.get(userId)) {
                if (tweetsMap.containsKey(followee) && 
                    tweetsMap.get(followee).size() > 0) {
                    maxHeap.offer(tweetsMap.get(followee).peekFirst());
                }
            }
        }

        for (int i = 0; i < 10 && !maxHeap.isEmpty(); i++) {
            Tweet tweet = maxHeap.poll();
            list.add(tweet.tweetId);
            if (tweet.prev != null) {
                maxHeap.offer(tweet.prev);
            }
        }
        
        return list;
    }
    
    /** Follower follows a followee. If the operation is invalid, it should be a no-op. */
    public void follow(int followerId, int followeeId) {
        // Can't follow yourself
        if (followerId == followeeId) {
            return;
        }
        if (!follows.containsKey(followerId)) {
            follows.put(followerId, new HashSet<Integer>());
        }
        follows.get(followerId).add(followeeId);
    }
    
    /** Follower unfollows a followee. If the operation is invalid, it should be a no-op. */
    public void unfollow(int followerId, int followeeId) {
        //unfollow not existing ones，unfollow not followed one
        if (!follows.containsKey(followerId) || 
            !follows.get(followerId).contains(followeeId)) {
            return;
        }
        
        follows.get(followerId).remove(followeeId);
    }
}

/**
 * Your Twitter object will be instantiated and called as such:
 * Twitter obj = new Twitter();
 * obj.postTweet(userId,tweetId);
 * List<Integer> param_2 = obj.getNewsFeed(userId);
 * obj.follow(followerId,followeeId);
 * obj.unfollow(followerId,followeeId);
 */
```

  


