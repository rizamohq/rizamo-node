# Reference
## Profiles
<details><summary><code>client.profiles.<a href="/src/api/resources/profiles/client/Client.ts">list</a>() -> Rizamo.ListProfilesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The brands or clients the team posts for, each with its colour and time zone. A key or person limited to some profiles gets those only.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.profiles.list();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `ProfilesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.profiles.<a href="/src/api/resources/profiles/client/Client.ts">create</a>({ ...params }) -> Rizamo.Profile</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

A brand or client of its own, with no accounts yet: connect them with `Get a link to connect an account`, or in the web app. Each profile's name is its own in the team (409 otherwise).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.profiles.create({
    name: "Bloom Studio",
    timeZone: "Europe/Lisbon"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.CreateProfilesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ProfilesClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.profiles.<a href="/src/api/resources/profiles/client/Client.ts">delete</a>({ ...params }) -> Rizamo.DeleteProfilesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

For good: what is in it cannot be restored. Its posts go, deleted ones included, with their history and preview links (posts already published stay on the networks), and so do its posting times, its upload requests and connect links, its other events, and its media that no post of another profile uses. Its short links stay and keep working, with no profile. People and invitations limited to some profiles, API keys, agents and webhook endpoints lose it from their profiles: a key or agent that reached only this profile is revoked, and an endpoint that took only its events is disabled (`disabledReason` `profile_deleted`). Refused (409) while it has accounts (move each to another profile, or remove it, first), when it is the team's only profile, while one of its posts is going out, and while a person or an open invitation reaches no other profile, naming them. Only an owner deletes a profile, signed in as themselves within the last 15 minutes (with their session, as the web app does), or an API key an owner let remove accounts and delete profiles when making it (Developers in the web app). Other API keys and agents are refused (403), and a key reaches only its own profiles.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.profiles.delete({
    id: "prof_01m41bamm0f3a8mr2eek4wdq39"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.DeleteProfilesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ProfilesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.profiles.<a href="/src/api/resources/profiles/client/Client.ts">update</a>({ ...params }) -> Rizamo.Profile</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Its name, colour or time zone; what is left out stays as it is. A new time zone reads posting times and local `scheduledAt` from then on: posts already scheduled keep their time.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.profiles.update({
    id: "prof_01m40k9k80fxd8cvng8derm7g9",
    color: "#3CCF96"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.UpdateProfilesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ProfilesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.profiles.<a href="/src/api/resources/profiles/client/Client.ts">queue</a>({ ...params }) -> Rizamo.Queue</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Its posting times, read in its time zone; the next `count` times free for at least one of its accounts, with which ones (none of them has a post at that minute, scheduled or queued, and none would pass its network's daily cap); and its queued posts still to go out.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.profiles.queue({
    id: "prof_01m40k9k80fxd8cvng8derm7g9"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.QueueProfilesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ProfilesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.profiles.<a href="/src/api/resources/profiles/client/Client.ts">setQueue</a>({ ...params }) -> Rizamo.Queue</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Replaces the profile's posting times with these, the whole week in one call; an empty list empties it. At most 24 a day, each once. Each is a local time in the profile's time zone, the same clock time all year. Posts already queued keep their times; only new ones take the new week.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.profiles.setQueue({
    id: "prof_01m40k9k80fxd8cvng8derm7g9",
    slots: [{
            weekday: "mon",
            time: "09:00"
        }, {
            weekday: "wed",
            time: "12:30"
        }, {
            weekday: "fri",
            time: "18:00"
        }]
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.SetQueueProfilesRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ProfilesClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Accounts
<details><summary><code>client.accounts.<a href="/src/api/resources/accounts/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Rizamo.Account, Rizamo.ListAccountsResponse&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Every account without `limit`; with it, a page at a time: pass `nextCursor` as `cursor` for the next one, with the same filters.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.accounts.list({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.accounts.list({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});
while (page.hasNextPage()) {
    page = await page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.ListAccountsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `AccountsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.accounts.<a href="/src/api/resources/accounts/client/Client.ts">get</a>({ ...params }) -> Rizamo.Account</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One connected account: its network, handle, profile, status, billing, what it can do (`capabilities`) and the formats it publishes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.accounts.get({
    id: "acc_01m423bp00fz39kp5pc7m42tsw"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.GetAccountsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `AccountsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.accounts.<a href="/src/api/resources/accounts/client/Client.ts">remove</a>({ ...params }) -> Rizamo.AccountRemoved</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

It stops publishing and is no longer billed, and nothing changes on its network. Its posts: one that goes to it alone moves to Deleted (`post.deleted`), scheduled, draft or published, and can be restored for 30 days; one with other accounts keeps them, loses this account's part that never went out (`post.updated`) and keeps the part that did, with its `url` and without its numbers (`accountRemoved` on the target). The answer counts them by status (`Preview removing an account` counts them before). Its name, picture and followers go at once; its handle stays to name those parts, with their links, for as long as their posts exist. What Rizamo read from the network about its posts there is deleted, and so are its comments and messages in the inbox, with the events that carry them (`comment.received`, `message.received`, `message.sent`, `comment_automation.*`) and their webhook deliveries. Its comment automations are paused (each with a `comment_automation.paused` event) and their runs deleted with the comments, so their numbers start again from zero and people they answered may be answered once more. It is told as `account.removed` with `reason` `removed_by_team`, never `account.disconnected`, which is a lost login. Connecting it again brings back the same account, its automations paused, to resume; posts in Deleted are restored by hand. Removing an account changes the bill, so only owners remove one, or an API key an owner let remove accounts and delete profiles when making it (Developers in the web app); other API keys are refused (403).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.accounts.remove({
    id: "acc_01m44bet40enpr62nh6w01e67r"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.RemoveAccountsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `AccountsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.accounts.<a href="/src/api/resources/accounts/client/Client.ts">update</a>({ ...params }) -> Rizamo.Account</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Moves the account to another profile you reach: from then on it is that profile's, for the people, keys and agents who reach it, and its old profile's stop seeing it. Events already written stay in the profile they happened in.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.accounts.update({
    id: "acc_01m423bp00fz39kp5pc7m42tsw",
    profileId: "prof_01m41bamm0f3a8mr2eek4wdq39"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.UpdateAccountsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `AccountsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.accounts.<a href="/src/api/resources/accounts/client/Client.ts">tiktokCreatorInfo</a>({ ...params }) -> Rizamo.TikTokCreatorInfo</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

What TikTok's posting screen needs, read from TikTok now: the creator's name and picture, who can see a photo post, whether the account turned comments, Duet or Stitch off, and the longest video it may post. TikTok asks apps to show the creator's name and these choices before every post.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.accounts.tiktokCreatorInfo({
    id: "acc_01m43kdrr0ebxa6wpz9f3zmaqa"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.TiktokCreatorInfoAccountsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `AccountsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.accounts.<a href="/src/api/resources/accounts/client/Client.ts">searchMusic</a>({ ...params }) -> Rizamo.SearchMusicAccountsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Tracks the account may put on a post, from its network's library. TikTok: its Commercial Music Library's trending list (up to 100), filtered by genre, country and period; there is no search. The same filters answer the same list for 30 minutes, and searches beyond Rizamo's limits on TikTok answer 429 with when to try again. Instagram (accounts connected through Facebook Login): a search with `q`, or what is trending without it, up to 25, music or original sounds. Facebook adds no music through its API. A filter of the other network is refused. Attach a track's `id` in the target's `music` option.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.accounts.searchMusic({
    id: "acc_01m43kdrr0ebxa6wpz9f3zmaqa",
    country: "PT"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.SearchMusicAccountsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `AccountsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.accounts.<a href="/src/api/resources/accounts/client/Client.ts">removal</a>({ ...params }) -> Rizamo.AccountRemoval</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

What removing the account would do to the posts that use it, counted now, with nothing changed: show it to the person before they confirm. `Remove an account` answers the same counts once it is done.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.accounts.removal({
    id: "acc_01m44bet40enpr62nh6w01e67r"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.RemovalAccountsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `AccountsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Connect
<details><summary><code>client.connect.<a href="/src/api/resources/connect/client/Client.ts">link</a>({ ...params }) -> Rizamo.ConnectLink</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

A link to send a person to within 30 minutes: it goes straight to the network, and connects accounts once (a preview or a second browser that opens it uses nothing up). They log in on the network, with no Rizamo account, and come back to `redirectUrl`, or, without one, land on a Rizamo page that says what was connected (for a chat agent, a script or n8n). `instagram` is Instagram Login, for an Instagram professional account on its own; `facebook` is Facebook Login, its Pages and the Instagram accounts linked to them, which can also add music to reels and get each story's final numbers when it ends (deleting Instagram posts will need it too, once Meta reviews Rizamo's access). LinkedIn connects in the web app only, as LinkedIn's terms ask: no connect link offers it. Once connected there, LinkedIn accounts publish and report through the API and MCP.

A login that reaches one new account the key may add connects it at once; one that reaches several (Pages, YouTube channels), or an account already in the team, shows the person a page to pick them, with only new accounts ticked. An account already in the team in a profile the key does not reach is never added. With `connectionId`, only that login's accounts are renewed.

Back at `redirectUrl`, Rizamo adds `status` (connected or error), `network`, `profileId`, and either `accountIds` with each one's `billing` in the same order, comma-separated, or `error` (cancelled, refused, no_accounts, expired, used, unavailable, forbidden, gone, failed) and `message`. Nothing in it works without your key: read the accounts with `GET /accounts/{id}`. A return can arrive more than once (a reload): take `GET /accounts` (`list_accounts`) as the truth. A link opened once it is used or expired, or after your key lost access, stays on a Rizamo page that says why: only a person back from the network comes to `redirectUrl`.

Accounts are billed as in the web app: the first 2 free. On the free plan the rest arrive `awaiting_payment` until an owner starts a plan. On a paid plan they are charged at once to the card on file: your call is the consent. A charge that needs the card holder, or more accounts than the owner lets the API add this period, leaves them `awaiting_payment` until an owner pays in the web app. The person connecting never sees prices.

With `connectionId`, the person logs in again for that login's accounts (an expired login): only accounts already in the team are updated, and `network` must be the login's.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.connect.link({
    network: "facebook",
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9",
    redirectUrl: "https://example.com/rizamo/connected"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.LinkConnectRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ConnectClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Fields
<details><summary><code>client.fields.<a href="/src/api/resources/fields/client/Client.ts">list</a>({ ...params }) -> Rizamo.ListFieldsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The team's custom fields, with their keys, types and choices: set them on posts with `fields`, and filter posts and analytics by them.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.fields.list();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.ListFieldsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `FieldsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.fields.<a href="/src/api/resources/fields/client/Client.ts">create</a>({ ...params }) -> Rizamo.FieldDefinition</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

A field every post can carry, such as a campaign. Its key and type cannot change, and a key is used once per team (409 otherwise).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.fields.create({
    key: "campaign",
    label: "Campaign",
    type: "select",
    options: ["Winter menu", "Brunch"],
    description: "The campaign a post belongs to."
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.CreateFieldsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `FieldsClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.fields.<a href="/src/api/resources/fields/client/Client.ts">delete</a>({ ...params }) -> Rizamo.DeleteFieldsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The field goes from the team, and its values are removed from every post.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.fields.delete({
    key: "campaign"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.DeleteFieldsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `FieldsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.fields.<a href="/src/api/resources/fields/client/Client.ts">update</a>({ ...params }) -> Rizamo.FieldDefinition</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The key and type cannot change. Removing an option leaves the value on posts that have it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.fields.update({
    key: "campaign",
    options: ["Winter menu", "Brunch", "Pastry week"]
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.UpdateFieldsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `FieldsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Posts
<details><summary><code>client.posts.<a href="/src/api/resources/posts/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Rizamo.Post, Rizamo.ListPostsResponse&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The team's posts, ordered by when they go out: their `scheduledAt`, or when they were created if they have none. The latest first, or the earliest first with `order` asc. A page at a time: pass `nextCursor` as `cursor` for the next one, with the same filters and `order`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.posts.list({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.posts.list({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});
while (page.hasNextPage()) {
    page = await page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.ListPostsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PostsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.posts.<a href="/src/api/resources/posts/client/Client.ts">create</a>({ ...params }) -> Rizamo.Post</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

A draft (the default), a post scheduled at `scheduledAt`, or one queued at its profile's next free posting time (`queue: true`), to one or more accounts of one profile. Each target is an account and a format, with its own text, files, options and first comment when it needs them. What a network would refuse is refused now with the reason, such as a first comment where the network takes none, or a story's own text on Instagram or Facebook; what only stops a post from going out, such as TikTok's choices on a draft, waits until it is scheduled. `Check a post without creating it` lists every problem at once. To publish now, create it, then `Publish a post now`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.posts.create({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9",
    text: "Winter menu is here: spiced orange latte and our first pastel de nata of the season. Open from 8 tomorrow.",
    targets: [{
            accountId: "acc_01m423bp00fz39kp5pc7m42tsw",
            format: "feed",
            firstComment: "Full menu: go.rizamo.com/k7Qm2p"
        }, {
            accountId: "acc_01m42vcqc0e15apwrdjth3v2q5"
        }, {
            accountId: "acc_01m44bet40enpr62nh6w01e67r",
            text: "Winter menu is here: spiced orange latte and our first pastel de nata of the season."
        }],
    mediaIds: ["med_01m48vn2c0emgvm8bkwtj1hayp"],
    scheduledAt: "2026-11-06T09:00:00Z",
    fields: {
        "campaign": "Winter menu"
    },
    status: "scheduled"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.CreatePostsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PostsClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.posts.<a href="/src/api/resources/posts/client/Client.ts">get</a>({ ...params }) -> Rizamo.Post</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One post with each target's status, link and error, and what Rizamo does to its files (`changes`). `List events` with its id has its history: why a target failed is in its `post.target.failed` event too.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.posts.get({
    id: "post_01m47bjzm0edmtk7w6gp7br39v"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.GetPostsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PostsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.posts.<a href="/src/api/resources/posts/client/Client.ts">delete</a>({ ...params }) -> Rizamo.Post</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The post is kept, marked deleted, and can be restored for 30 days, then goes for good unless a target is still live on its network. Live targets are removed from their networks where they allow it: each target's `removal` says what happened. Deleting it again retries the ones that failed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.posts.delete({
    id: "post_01m47bjzm0edmtk7w6gp7br39v"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.DeletePostsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PostsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.posts.<a href="/src/api/resources/posts/client/Client.ts">update</a>({ ...params }) -> Rizamo.UpdatePostsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Changes its text, files, chain, time, targets or fields, schedules a draft (`status` scheduled with a future `scheduledAt`, or `queue: true`), or moves a scheduled post back to draft; what is left out stays as it is. Targets already live change on their network only with `applyToPublished`, where the network allows it, and `edits` says what happened to each.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.posts.update({
    id: "post_01m47bjzm0edmtk7w6gp7br39v",
    scheduledAt: "2026-11-06T10:30:00Z",
    timeZone: "Europe/Lisbon"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.UpdatePostsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PostsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.posts.<a href="/src/api/resources/posts/client/Client.ts">validate</a>({ ...params }) -> Rizamo.ValidatePostsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Takes what Create a post takes and creates nothing. `problems` are what would stop it now; `warnings` are what would stop it from being scheduled or published later, such as Instagram without an image or a video. Each target says what Rizamo would do to its files, and `scheduledAt` when it would go out (with `queue: true`, the queue's next time free for all of its accounts).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.posts.validate({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9",
    text: "Winter menu is here: spiced orange latte and our first pastel de nata of the season. Open from 8 tomorrow.",
    targets: [{
            accountId: "acc_01m423bp00fz39kp5pc7m42tsw",
            format: "reel"
        }, {
            accountId: "acc_01m423bp00fz39kp5pc7m42tsw",
            format: "story"
        }, {
            accountId: "acc_01m43kdrr0ebxa6wpz9f3zmaqa"
        }],
    mediaIds: ["med_01m49kp3r0ed9szw9jcadbjdp1"],
    status: "draft"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.ValidatePostsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PostsClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.posts.<a href="/src/api/resources/posts/client/Client.ts">publish</a>({ ...params }) -> Rizamo.Post</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Every target that is not live goes out now, failed ones included. A draft or scheduled post becomes scheduled for now; follow each target's `status` until it is `published` or `failed`. Targets whose result is `unknown` are left alone: check the network first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.posts.publish({
    id: "post_01m47bjzm0edmtk7w6gp7br39v"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.PublishPostsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PostsClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.posts.<a href="/src/api/resources/posts/client/Client.ts">restore</a>({ ...params }) -> Rizamo.Post</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Within 30 days of deleting it. A scheduled post whose time has passed, or with a target whose account is no longer in its profile (moved to another), comes back as a draft. A post moved to Deleted because its account was removed comes back as it was: its parts on that account (`accountRemoved`) go out only once the account is connected again. Until then they fail at their time, saying why, and scheduling or publishing the post is refused.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.posts.restore({
    id: "post_01m47bjzm0edmtk7w6gp7br39v"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.RestorePostsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PostsClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.posts.<a href="/src/api/resources/posts/client/Client.ts">share</a>({ ...params }) -> Rizamo.SharePostsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a page anyone with the link can open without signing in: the post as it will look on each of its accounts, and nothing else about it. The link works for 30 days. Sharing again makes a new link and gives every link of the post that still works 30 more days. Stopping the share or deleting the post turns them all off.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.posts.share({
    id: "post_01m47bjzm0edmtk7w6gp7br39v"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.SharePostsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PostsClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.posts.<a href="/src/api/resources/posts/client/Client.ts">unshare</a>({ ...params }) -> Rizamo.Post</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Every preview link of the post stops working at once. `sharedUntil` becomes null.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.posts.unshare({
    id: "post_01m47bjzm0edmtk7w6gp7br39v"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.UnsharePostsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `PostsClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Network posts
<details><summary><code>client.networkPosts.<a href="/src/api/resources/networkPosts/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Rizamo.NetworkPost, Rizamo.ListNetworkPostsResponse&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Every post on the team's connected accounts, whoever made it: published through Rizamo (`origin` rizamo, with its `postId`) or in the network's own apps (`external`). Newest first, a page at a time: pass `nextCursor` as `cursor` for the next one. Rizamo finds new posts within the hour; when an account is connected it reads back 12 months. A LinkedIn profile's posts made outside Rizamo are not listed, as LinkedIn lists them to select developers only. Each post has its latest metrics, read 1 hour and 6 hours after it went out (TikTok's and YouTube's from 24 hours, as their numbers come a day or more late), then daily to day 90 and every 30 days after (YouTube every 28).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.networkPosts.list({
    accountId: "acc_01m423bp00fz39kp5pc7m42tsw"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.networkPosts.list({
    accountId: "acc_01m423bp00fz39kp5pc7m42tsw"
});
while (page.hasNextPage()) {
    page = await page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.ListNetworkPostsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworkPostsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.networkPosts.<a href="/src/api/resources/networkPosts/client/Client.ts">get</a>({ ...params }) -> Rizamo.NetworkPost</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One post on a network, made through Rizamo or anywhere else: its caption, link and format, the Rizamo post it went out as, whether it is still on the network, its latest numbers with when they were read, and its `details` (rates, traffic sources, viewer types, retention, viewers) where its network gives them.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.networkPosts.get({
    id: "npost_01m4fkyer0em9939e5rz4f89v7"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.GetNetworkPostsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworkPostsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.networkPosts.<a href="/src/api/resources/networkPosts/client/Client.ts">timeline</a>({ ...params }) -> Rizamo.NetworkPostTimeline</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

What each day added to the post's numbers, and the totals after it, from Rizamo's reads: 1 hour and 6 hours after it went out (TikTok's and YouTube's from 24 hours), then daily to day 90 and every 30 days after (YouTube every 28). A day with no point had no change. A change between two reads several days apart is one point over those days, never split, and `gaps` says why, as it does for days Rizamo could not read. Days are the profile's.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.networkPosts.timeline({
    id: "npost_01m4fkyer0em9939e5rz4f89v7"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.TimelineNetworkPostsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `NetworkPostsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Media
<details><summary><code>client.media.<a href="/src/api/resources/media/client/Client.ts">create</a>({ ...params }) -> Rizamo.CreateMediaResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

With `contentType` and `size` (up to 4 GB), the answer says where to send the file: PUT each part, then call `complete` if there is one, and the media is `ready`. With `url`, Rizamo downloads the file and the media is ready in the answer. Media is yours until a post uses it, and then belongs to that post's profile (or to `profileId` at once): keys and people limited to some profiles reach their own media and their profiles'. Media not used by a post within 7 days is deleted.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.media.create({
    contentType: "video/mp4",
    size: 48211334,
    alt: "Pouring latte art in slow motion",
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.CreateMediaRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `MediaClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.media.<a href="/src/api/resources/media/client/Client.ts">get</a>({ ...params }) -> Rizamo.Media</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One image or video: `ready` once its file arrived, with its size, dimensions and length, and a link to view it that works for a few hours.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.media.get({
    id: "med_01m48vn2c0emgvm8bkwtj1hayp"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.GetMediaRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `MediaClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Uploads
<details><summary><code>client.uploads.<a href="/src/api/resources/uploads/client/Client.ts">create</a>({ ...params }) -> Rizamo.UploadRequest</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a page to give a person. They add images or videos there, no sign-in needed, and send them. Follow `status` with Get an upload request; its `media` are ready to use on a post. The page works for 24 hours.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.uploads.create({
    note: "The photos from Saturday's tasting",
    maxFiles: 10,
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.CreateUploadsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `UploadsClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.uploads.<a href="/src/api/resources/uploads/client/Client.ts">get</a>({ ...params }) -> Rizamo.UploadRequest</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Whether the person sent their files: `done` once they did, with `media` ready to put on a post. Its page's address is only in the answer that created it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.uploads.get({
    id: "upr_01m4abq540fy78hvv8x8xs62tm"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.GetUploadsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `UploadsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Links
<details><summary><code>client.links.<a href="/src/api/resources/links/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Rizamo.Link, Rizamo.ListLinksResponse&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Newest first, a page at a time: pass `nextCursor` as `cursor` for the next one.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.links.list({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.links.list({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});
while (page.hasNextPage()) {
    page = await page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.ListLinksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LinksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.links.<a href="/src/api/resources/links/client/Client.ts">create</a>({ ...params }) -> Rizamo.Link</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

A short address on Rizamo's link host that sends people on to `url` and counts each click, by day and country. Nothing about the person who clicks is kept: no IP address, cookie or device. Link previews (Instagram, Facebook, WhatsApp, Slack, X and others) and bots are not counted. Without `profileId`, the link is yours (the person, key or agent that made it) and people limited to some profiles do not see it. A team makes up to 1,000 links in 24 hours, and only once it has a connected account or a paid plan (403 until then).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.links.create({
    url: "https://cafelumen.pt/menu",
    utm: {
        source: "instagram",
        medium: "social",
        campaign: "winter-menu"
    },
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.CreateLinksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LinksClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.links.<a href="/src/api/resources/links/client/Client.ts">get</a>({ ...params }) -> Rizamo.GetLinksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One short link, with its clicks so far, per day (UTC) and per country.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.links.get({
    id: "lnk_01m4b3r6g0e48txnypr2tcytdp"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.GetLinksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LinksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.links.<a href="/src/api/resources/links/client/Client.ts">delete</a>({ ...params }) -> Rizamo.DeleteLinksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

It stops working within a minute everywhere it was shared (at most 11 minutes in a place under heavy load), and its click counts are deleted.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.links.delete({
    id: "lnk_01m4b3r6g0e48txnypr2tcytdp"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.DeleteLinksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LinksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.links.<a href="/src/api/resources/links/client/Client.ts">update</a>({ ...params }) -> Rizamo.Link</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

A new `url` applies to every click from now on, wherever the link was shared; it can take a minute to reach every place, at most 11 minutes in one under heavy load. `expiresAt` null makes it never expire. A new `url` needs the team to have a connected account or a paid plan, as making a link does.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.links.update({
    id: "lnk_01m4b3r6g0e48txnypr2tcytdp",
    expiresAt: "2026-12-31T23:59:59Z"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.UpdateLinksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `LinksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Inbox
<details><summary><code>client.inbox.<a href="/src/api/resources/inbox/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Rizamo.Thread, Rizamo.ListInboxResponse&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One thread per first comment, with the replies under it, and one per person for messages. Those with the newest messages first, 200 at a time unless `limit` says fewer: pass `nextCursor` as `cursor` for the next page, with the same filters.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.inbox.list();
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.inbox.list();
while (page.hasNextPage()) {
    page = await page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.ListInboxRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `InboxClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.inbox.<a href="/src/api/resources/inbox/client/Client.ts">posts</a>({ ...params }) -> core.Page&lt;Rizamo.InboxPost, Rizamo.PostsInboxResponse&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The posts on the team's accounts that have comment threads, the most recently commented first, each with its threads counted. A page at a time, 100 unless `limit` says fewer: pass `nextCursor` as `cursor` for the next one, with the same filters.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.inbox.posts({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.inbox.posts({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});
while (page.hasNextPage()) {
    page = await page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.PostsInboxRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `InboxClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.inbox.<a href="/src/api/resources/inbox/client/Client.ts">get</a>({ ...params }) -> Rizamo.GetInboxResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Its messages oldest first: every one without `limit`; with it, the newest `limit`, and `nextCursor`, passed as `before`, gives the ones before them.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.inbox.get({
    id: "thr_01m4bvs7w0fmf9g0mrdy7j6bc5"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.GetInboxRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `InboxClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.inbox.<a href="/src/api/resources/inbox/client/Client.ts">update</a>({ ...params }) -> Rizamo.Thread</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Marks it done or open, read or unread, or hands it to a teammate who reaches its profile (`assigneeId`). Nothing is sent to the network.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.inbox.update({
    id: "thr_01m4bvs7w0fmf9g0mrdy7j6bc5",
    status: "done"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.UpdateInboxRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `InboxClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.inbox.<a href="/src/api/resources/inbox/client/Client.ts">reply</a>({ ...params }) -> Rizamo.Message</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Answers as the account: publicly under the comment, or in a private message within 24 hours of the person's last one (`replyWindowEndsAt`). A Threads, LinkedIn or YouTube reply comes back `sending` and goes out within a minute: read the thread to follow it. One that failed says why in `deliveryError`; `retryOf` tries it once more, never sending it twice.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.inbox.reply({
    id: "thr_01m4bvs7w0fmf9g0mrdy7j6bc5",
    text: "It is, Marta! Oat, almond or soy, at no extra cost."
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.ReplyInboxRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `InboxClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.inbox.<a href="/src/api/resources/inbox/client/Client.ts">markPostDone</a>({ ...params }) -> Rizamo.MarkPostDoneInboxResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Every comment thread on the post that is open or unread, and whose newest message is no later than `before`, becomes done and read, as Update a thread would one by one. A thread with something newer stays as it is, and a comment that arrives later opens its thread again.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.inbox.markPostDone({
    id: "npost_01m4fkyer0em9939e5rz4f89v7",
    before: "2026-11-06T10:14:00Z"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.MarkPostDoneInboxRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `InboxClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.inbox.<a href="/src/api/resources/inbox/client/Client.ts">deleteComment</a>({ ...params }) -> Rizamo.DeleteCommentInboxResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes the comment from its network, as the account, with the replies under it, and from the thread: it no longer shows in `Get a thread`. When it is the thread's first comment (`first`), the thread goes too, and leaves every list and count. One already gone from the network counts as deleted, so a delete that failed can be asked again. Errors: 400, before any call, when it is not a comment (a message) or its network does not allow it for this comment, with why (`moderationProblem`); 422 `capability_missing` when the account's login does not allow managing comments (on Threads, until Meta approves Rizamo's access to replies); 409 when the account needs a new login or is not active, the reply is still sending, or the network refused, with its reason; 404 for a thread or comment the caller does not reach. On Threads, 422 too for the profile's own reply until Meta approves Rizamo's access to deletes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.inbox.deleteComment({
    id: "thr_01m4bvs7w0fmf9g0mrdy7j6bc5",
    messageId: "msg_01m4e3wc00ecj9ez6jrr2c6eaj"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.DeleteCommentInboxRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `InboxClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.inbox.<a href="/src/api/resources/inbox/client/Client.ts">hideComment</a>({ ...params }) -> Rizamo.Message</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Hides the comment on its network, as the account, or shows it again (`hidden: false`), then records it on the message. The account's own comments are never hidden, and on Threads only first-level replies (`first`), which hide the replies under them too. Errors: 400, before any call, when it is not a comment (a message) or its network does not allow it for this comment, with why (`moderationProblem`); 422 `capability_missing` when the account's login does not allow managing comments (on Threads, until Meta approves Rizamo's access to replies); 409 when the account needs a new login or is not active, the reply is still sending, or the network refused, with its reason; 404 for a thread or comment the caller does not reach.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.inbox.hideComment({
    id: "thr_01m4bvs7w0fmf9g0mrdy7j6bc5",
    messageId: "msg_01m4dbvam0e87bh8nfk28wrqne",
    hidden: true
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.HideCommentInboxRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `InboxClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.inbox.<a href="/src/api/resources/inbox/client/Client.ts">likeComment</a>({ ...params }) -> Rizamo.Message</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Likes the comment as the Facebook or LinkedIn Page, or takes the like back (`liked: false`), then records it on the message. Comments on Facebook or LinkedIn Pages only, by others than the Page. Errors: 400, before any call, when it is not a comment (a message) or its network does not allow it for this comment, with why (`moderationProblem`); 422 `capability_missing` when the account's login does not allow managing comments (on Threads, until Meta approves Rizamo's access to replies); 409 when the account needs a new login or is not active, the reply is still sending, or the network refused, with its reason; 404 for a thread or comment the caller does not reach.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.inbox.likeComment({
    id: "thr_01m4ckt980em09vyrhvr9tf4am",
    messageId: "msg_01m4evxdc0fbt8xh2rc4hhptg1",
    liked: true
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.LikeCommentInboxRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `InboxClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Members
<details><summary><code>client.members.<a href="/src/api/resources/members/client/Client.ts">list</a>() -> Rizamo.ListMembersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The team's people who share a profile with you, or reach every profile, with their profiles narrowed to yours: whom to assign an inbox thread to. No emails. People are invited, changed and removed by owners in the web app.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.members.list();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `MembersClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Comment automations
<details><summary><code>client.commentAutomations.<a href="/src/api/resources/commentAutomations/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Rizamo.CommentAutomation, Rizamo.ListCommentAutomationsResponse&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Newest first, with their numbers so far. Every one without `limit`; with it, a page at a time: pass `nextCursor` as `cursor` for the next one, with the same filters.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.commentAutomations.list({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.commentAutomations.list({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});
while (page.hasNextPage()) {
    page = await page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.ListCommentAutomationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CommentAutomationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.commentAutomations.<a href="/src/api/resources/commentAutomations/client/Client.ts">create</a>({ ...params }) -> Rizamo.CommentAutomation</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

A comment that matches a keyword, on one post or on any post of an Instagram account or Facebook Page, gets a private reply with the message and its link behind a button, once per person by default. Optionally one of up to 5 public replies is posted under it afterwards, and its thread is marked done. On Instagram a follow gate can ask them to follow and reply first, with a button that replies for them. Only top-level comments from others count, made after the automation starts; Rizamo reads comments every few minutes, so answers go out within minutes. Meta takes one private reply per comment, within 7 days of it. An account sends a set number of automated messages a day at most (`dailyCap` in the numbers), paced well under Meta's limits. Not on TikTok: automations answer by private message, and TikTok does not offer its messaging API to accounts in the EEA, Switzerland or the UK, so a TikTok account is refused with that reason.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.commentAutomations.create({
    name: "Winter menu guide",
    keywords: ["menu", "guide"],
    message: {
        text: "Here is our winter menu, with every drink and pastry of the season.",
        link: "https://cafelumen.pt/menu",
        button: "See the menu"
    },
    publicReplies: ["Sent it to your messages!", "Check your DMs!"],
    markDone: true,
    accountId: "acc_01m423bp00fz39kp5pc7m42tsw",
    networkPostId: "npost_01m4fkyer0em9939e5rz4f89v7"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.CreateCommentAutomationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CommentAutomationsClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.commentAutomations.<a href="/src/api/resources/commentAutomations/client/Client.ts">get</a>({ ...params }) -> Rizamo.CommentAutomation</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One comment automation: its settings, whether it is armed or paused and why, and its numbers so far.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.commentAutomations.get({
    id: "cauto_01m4h40hg0f4wa1w5cfcgpjrp3"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.GetCommentAutomationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CommentAutomationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.commentAutomations.<a href="/src/api/resources/commentAutomations/client/Client.ts">delete</a>({ ...params }) -> Rizamo.DeleteCommentAutomationsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

It stops at once, with its runs. Messages already sent stay in the inbox.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.commentAutomations.delete({
    id: "cauto_01m4h40hg0f4wa1w5cfcgpjrp3"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.DeleteCommentAutomationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CommentAutomationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.commentAutomations.<a href="/src/api/resources/commentAutomations/client/Client.ts">update</a>({ ...params }) -> Rizamo.CommentAutomation</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The account and post cannot change. Pausing stops it at once; comments made while it is paused are never answered. Resuming starts from then.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.commentAutomations.update({
    id: "cauto_01m4h40hg0f4wa1w5cfcgpjrp3",
    status: "paused"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.UpdateCommentAutomationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CommentAutomationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.commentAutomations.<a href="/src/api/resources/commentAutomations/client/Client.ts">runs</a>({ ...params }) -> core.Page&lt;Rizamo.CommentAutomationRun, Rizamo.RunsCommentAutomationsResponse&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

One run per matched comment, newest first, a page at a time: pass `nextCursor` as `cursor` for the next one. A run stays when its comment is deleted, but its `threadId` may then be gone from the inbox, and a private reply not sent yet is skipped (`refused`).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.commentAutomations.runs({
    id: "cauto_01m4h40hg0f4wa1w5cfcgpjrp3"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.commentAutomations.runs({
    id: "cauto_01m4h40hg0f4wa1w5cfcgpjrp3"
});
while (page.hasNextPage()) {
    page = await page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.RunsCommentAutomationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CommentAutomationsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.commentAutomations.<a href="/src/api/resources/commentAutomations/client/Client.ts">test</a>({ ...params }) -> Rizamo.CommentAutomationTest</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Whether a comment with this text would trigger it, and the messages it would send, with their Rizamo links: each as its text and its button (the link, or the follow gate's reply button). Nothing is sent or recorded. Whether the person already got it, follows the account or is within Meta's windows is only known for real comments.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.commentAutomations.test({
    id: "cauto_01m4h40hg0f4wa1w5cfcgpjrp3",
    text: "Menu please!"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.TestCommentAutomationsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `CommentAutomationsClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Analytics
<details><summary><code>client.analytics.<a href="/src/api/resources/analytics/client/Client.ts">overview</a>({ ...params }) -> Rizamo.AnalyticsOverview</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The numbers of the team's accounts and of every post on them, made in Rizamo or anywhere else, for a period and the one before it: views, reach, engagements, the engagement rate of the posts published, posts published, followers, the accounts' own reach and accounts engaged, each day, each network, and the top posts. A period of `days` ends yesterday, the last complete day, as `to` does when left out. With `attribution` received (the default), views are each account's own views of each day, as its network counts them (its posts' gains where its days give none, and with `fields`), and reach and engagements what arrived on the posts in the period, on posts of any age, by the day it arrived; with publish, they are the numbers so far of the posts published in the period, by the day each went out. A number a network does not give is missing, never 0, and `notes` says why. Post numbers follow the days of the profile's time zone (pass `timeZone` for another); followers and the accounts' own numbers come by the network's days, matched by date (Meta's run on Pacific time, TikTok's on UTC). TikTok's days come 2 days late and YouTube's 3.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.analytics.overview({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.OverviewAnalyticsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `AnalyticsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.analytics.<a href="/src/api/resources/analytics/client/Client.ts">posts</a>({ ...params }) -> Rizamo.PostsAnalyticsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Every post published in the period on the team's accounts, made in Rizamo or anywhere else, deleted ones included, with its numbers so far: its lifetime totals as Rizamo last read them, every one its network gives in `metrics`, and its `details` (rates, traffic sources, viewer types, retention, viewers) where its network gives them. Sorted by views unless asked otherwise, a page at a time. Days are the profile's, and a period of `days` ends yesterday, as in Analytics overview.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.analytics.posts({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.PostsAnalyticsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `AnalyticsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.analytics.<a href="/src/api/resources/analytics/client/Client.ts">audience</a>({ ...params }) -> Rizamo.Audience</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Each account's audience as last read: its followers, and the people who engaged with its content this month, by age, gender, country and city (LinkedIn without age or gender, and by industry, job function, seniority and company size; YouTube without city), and when its followers are active, by the hour in UTC (`activeHours`), from TikTok, for accounts with advanced access or a verified business account, and 100 followers or more. Rizamo reads it once a week for Instagram, TikTok, Threads, LinkedIn and YouTube accounts (Instagram through either login). Followers come only for accounts with 100 followers or more. Instagram gives the engaged audience only when each group has more than 100 people; TikTok, Threads and LinkedIn give none; YouTube gives no followers (`followers` is null). A YouTube channel's engaged audience is its viewers this month (last month until the 8th, as YouTube's numbers come 2 to 3 days late), counted by their views. Facebook no longer gives a Page's audience, and other networks are not read yet: their accounts come with why.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.analytics.audience({
    profileId: "prof_01m40k9k80fxd8cvng8derm7g9"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.AudienceAnalyticsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `AnalyticsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Billing
<details><summary><code>client.billing.<a href="/src/api/resources/billing/client/Client.ts">get</a>() -> Rizamo.Billing</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Billed per connected account, the first 2 free. Only keys and people that reach every profile see it, since the plan counts every profile's accounts.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.billing.get();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `BillingClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Events
<details><summary><code>client.events.<a href="/src/api/resources/events/client/Client.ts">list</a>({ ...params }) -> core.Page&lt;Rizamo.Event, Rizamo.ListEventsResponse&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Every change on the team's posts and accounts in the last 30 days, newest first, with who made it: a person, an API key, an agent, or Rizamo itself; and the inbox's comments and messages as they arrive, the replies sent from Rizamo, and what comment automations do. The same events webhooks send, each as one item of this list. A page at a time: pass `nextCursor` as `cursor` for the next one. Someone limited to some profiles sees only those profiles' events. The inbox's and comment automations' events carry what people wrote: a key or agent reads them only with `inbox:read` (`comment.received`, `message.received`, `message.sent`) or `automations:read` (`comment_automation.*`) too; asking for one of those types without it answers 403.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.events.list({
    resourceId: "post_01m47bjzm0edmtk7w6gp7br39v"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.events.list({
    resourceId: "post_01m47bjzm0edmtk7w6gp7br39v"
});
while (page.hasNextPage()) {
    page = await page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.ListEventsRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `EventsClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Webhooks
<details><summary><code>client.webhooks.<a href="/src/api/resources/webhooks/client/Client.ts">list</a>() -> Rizamo.ListWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

The team's endpoints, oldest first, without their signing secrets. An owner sees every one, also through their agent or their API key; anyone else only those that send for them (`onBehalfOf`). Someone limited to some profiles sees only endpoints limited to those profiles.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.list();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `WebhooksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.<a href="/src/api/resources/webhooks/client/Client.ts">create</a>({ ...params }) -> Rizamo.WebhookSecret</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Events from now on go to it, of the profiles the person it sends for reaches (`onBehalfOf`: the caller, or the person behind the API key or agent), and it is deleted when they leave the team. Each event goes as one POST of JSON (the event as `List events` gives it), signed with Standard Webhooks' headers (`webhook-id`, the event's id; `webhook-timestamp`; `webhook-signature`). A 2xx answer within 15 seconds is delivered; anything else is tried again 6 times over about 18 hours, and a 410 Gone disables the endpoint. After 10 failures in a row an endpoint's deliveries wait while one at a time tries it, and one that keeps failing like that with nothing delivered for 5 days is disabled; Rizamo emails the team's owners and the person it sends for. Never sent to rizamo.com or workers.dev addresses, nor to private ones. Deliveries are not in order: order one resource's events by `at`. Its signing secret is in the answer, and only there. A team has up to 20 endpoints.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.create({
    url: "https://hooks.cafelumen.pt/rizamo",
    description: "Posts to our CRM",
    events: ["post.published", "post.failed", "post.target.failed"]
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.CreateWebhooksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `WebhooksClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.<a href="/src/api/resources/webhooks/client/Client.ts">delete</a>({ ...params }) -> Rizamo.DeleteWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Nothing more is sent to it, and its deliveries are deleted with it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.delete({
    id: "wh_01m4m44q00ea9a11gpjs99ddcy"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.DeleteWebhooksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `WebhooksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.<a href="/src/api/resources/webhooks/client/Client.ts">update</a>({ ...params }) -> Rizamo.WebhookEndpoint</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Changes apply to events from now on, and to deliveries still waiting for a retry: each is checked against the endpoint as it is when its turn comes. A delivery whose event the endpoint no longer takes (its new types or profiles) ends unsent, with `endpoint_changed` on its attempt; the ones it still takes go to its new `url`. A new `url` starts with a closed breaker, makes the caller (or the person behind the API key or agent) the person it sends for (so does any change to one that sends for nobody, `onBehalfOf` null), and the deliveries it had already tried or held at the old address end with `endpoint_changed` (replay them to send them to the new one). `enabled` false stops it, and its waiting deliveries end at once with `endpoint_disabled`; true starts it again for new events, also after a 410 Gone or days of failures, with its failures forgotten. What ended while it was off is not sent by itself: replay it (`Replay an endpoint's deliveries`).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.update({
    id: "wh_01m4m44q00ea9a11gpjs99ddcy"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.UpdateWebhooksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `WebhooksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.<a href="/src/api/resources/webhooks/client/Client.ts">rotateSecret</a>({ ...params }) -> Rizamo.WebhookSecret</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

A new signing secret, in the answer and only there. For 24 hours each delivery carries two signatures in `webhook-signature`, one with each secret, so the receiver can switch without losing any; then only the new one.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.rotateSecret({
    id: "wh_01m4m44q00ea9a11gpjs99ddcy"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.RotateSecretWebhooksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `WebhooksClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.<a href="/src/api/resources/webhooks/client/Client.ts">test</a>({ ...params }) -> Rizamo.WebhookDelivery</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

A delivery of type `webhook.test` sent now, signed as every delivery is, and its attempt in the answer. It is tried once, never retried, and shows in the deliveries. A disabled endpoint can be tested. A team sends up to 10 tests a minute; more answer 429.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.test({
    id: "wh_01m4m44q00ea9a11gpjs99ddcy"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.TestWebhooksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `WebhooksClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.<a href="/src/api/resources/webhooks/client/Client.ts">deliveries</a>({ ...params }) -> core.Page&lt;Rizamo.WebhookDelivery, Rizamo.DeliveriesWebhooksResponse&gt;</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Each event (and test) sent to an endpoint, newest first, with every attempt, from the last 30 days. A page at a time: pass `nextCursor` as `cursor` for the next one. Only deliveries of endpoints the caller sees; someone limited to some profiles sees only their profiles' events among them, and tests. Each payload is an event as `List events` shows it, so `webhooks:read` reads what `events:read` reads: the inbox's and comment automations' deliveries only with `inbox:read` or `automations:read` too.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
const pageableResponse = await client.webhooks.deliveries({
    endpointId: "wh_01m4m44q00ea9a11gpjs99ddcy"
});
for await (const item of pageableResponse) {
    console.log(item);
}

// Or you can manually iterate page-by-page
let page = await client.webhooks.deliveries({
    endpointId: "wh_01m4m44q00ea9a11gpjs99ddcy"
});
while (page.hasNextPage()) {
    page = await page.getNextPage();
}

// You can also access the underlying response
const response = page.response;

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.DeliveriesWebhooksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `WebhooksClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.<a href="/src/api/resources/webhooks/client/Client.ts">replay</a>({ ...params }) -> Rizamo.WebhookDelivery</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends a delivery again, once and now, through the queue: the body it sent before (made from its event when it never went), signed anew, with the same `webhook-id` (the event's id), so a receiver that has it already can skip it. One more attempt, to the endpoint's `url` as it is now, never retried; it shows among the delivery's attempts. The endpoint must still take the event (its types and profiles now) and be enabled. A delivery still waiting for a retry is refused: it goes on its own. A team replays up to 5,000 deliveries an hour, one at a time and by range together; more answer 429.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.replay({
    id: "whd_01m4mw5rc0ehs83dnfzc56pd0g"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.ReplayWebhooksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `WebhooksClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.<a href="/src/api/resources/webhooks/client/Client.ts">replayRange</a>({ ...params }) -> Rizamo.WebhookReplay</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends again, once each and now, the endpoint's deliveries made between `since` and `until` (within the last 30 days): the failed ones, or every one with `status` all. Each keeps its `webhook-id` and goes to the endpoint's `url` as it is now. Deliveries the endpoint no longer takes are skipped, and those still waiting for a retry are not replayed. Up to 1,000 a call, in the order they were made, and within the team's 5,000 replays an hour (429 once none are left); `more` says the range holds more, and `nextCursor` continues after the last one this call looked at. One range at a time: a call while the endpoint's last replay is still being sent answers 409. The endpoint must be enabled.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.webhooks.replayRange({
    id: "wh_01m4m44q00ea9a11gpjs99ddcy",
    since: "2026-11-06T00:00:00Z"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `Rizamo.ReplayRangeWebhooksRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `WebhooksClient.IdempotentRequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

