these are just some notes I took during development of this

# actors

https://www.w3.org/TR/activitypub/#actor-objects

https://seb.jambor.dev/posts/understanding-activitypub/

this is basically the person's profile

```
❯ curl -s https://simian.rodeo/.well-known/webfinger\?resource\=acct:kitchen@simian.rodeo | jq .
{
  "subject": "acct:kitchen@simian.rodeo",
  "aliases": [
    "https://simian.rodeo/@kitchen",
    "https://simian.rodeo/users/kitchen"
  ],
  "links": [
    {
      "rel": "http://webfinger.net/rel/profile-page",
      "type": "text/html",
      "href": "https://simian.rodeo/@kitchen"
    },
    {
      "rel": "self",
      "type": "application/activity+json",
      "href": "https://simian.rodeo/users/kitchen"
    },
    {
      "rel": "http://ostatus.org/schema/1.0/subscribe",
      "template": "https://simian.rodeo/authorize_interaction?uri={uri}"
    }
  ]
}
```

ok, and everywhere says "set the header: application/ld+json" something something but nothing tells you 
*which* header to set to that value.

But finally, this page did: https://docs.gitlab.com/ee/development/activitypub/actors/

Accept.

```
  curl -H 'Accept: application/ld+json; profile="https://www.w3.org/ns/activitystreams"' curl --header 'application/ld+json; profile="https://www.w3.org/ns/activitystreams"' https://simian.rodeo/users/kitchen | jq .
  {
  "@context": [
    "https://www.w3.org/ns/activitystreams",
    "https://w3id.org/security/v1",
    {
      "manuallyApprovesFollowers": "as:manuallyApprovesFollowers",
      "toot": "http://joinmastodon.org/ns#",
      "featured": {
        "@id": "toot:featured",
        "@type": "@id"
      },
      "featuredTags": {
        "@id": "toot:featuredTags",
        "@type": "@id"
      },
      "alsoKnownAs": {
        "@id": "as:alsoKnownAs",
        "@type": "@id"
      },
      "movedTo": {
        "@id": "as:movedTo",
        "@type": "@id"
      },
      "schema": "http://schema.org#",
      "PropertyValue": "schema:PropertyValue",
      "value": "schema:value",
      "discoverable": "toot:discoverable",
      "Device": "toot:Device",
      "Ed25519Signature": "toot:Ed25519Signature",
      "Ed25519Key": "toot:Ed25519Key",
      "Curve25519Key": "toot:Curve25519Key",
      "EncryptedMessage": "toot:EncryptedMessage",
      "publicKeyBase64": "toot:publicKeyBase64",
      "deviceId": "toot:deviceId",
      "claim": {
        "@type": "@id",
        "@id": "toot:claim"
      },
      "fingerprintKey": {
        "@type": "@id",
        "@id": "toot:fingerprintKey"
      },
      "identityKey": {
        "@type": "@id",
        "@id": "toot:identityKey"
      },
      "devices": {
        "@type": "@id",
        "@id": "toot:devices"
      },
      "messageFranking": "toot:messageFranking",
      "messageType": "toot:messageType",
      "cipherText": "toot:cipherText",
      "suspended": "toot:suspended",
      "Hashtag": "as:Hashtag",
      "focalPoint": {
        "@container": "@list",
        "@id": "toot:focalPoint"
      }
    }
  ],
  "id": "https://simian.rodeo/users/kitchen",
  "type": "Person",
  "following": "https://simian.rodeo/users/kitchen/following",
  "followers": "https://simian.rodeo/users/kitchen/followers",
  "inbox": "https://simian.rodeo/users/kitchen/inbox",
  "outbox": "https://simian.rodeo/users/kitchen/outbox",
  "featured": "https://simian.rodeo/users/kitchen/collections/featured",
  "featuredTags": "https://simian.rodeo/users/kitchen/collections/tags",
  "preferredUsername": "kitchen",
  "name": "Jeremy Kitchen",
  "summary": "<p>On a break from my 5 year world tour.</p><p>Recently diagnosed with colon cancer so a lot of my posts now are going to be about that. I’ll CW any super graphic stuff but consider this a CW: cancer for my entire feed.</p><p>Currently: 🇺🇸<br />Previously: 🇯🇵🇰🇷🇹🇼🇳🇿🇳🇱</p><p>I love cats. And dogs.</p><p>Estoy aprendiendo Español.</p><p>Awkwardly searchable.</p><p><a href=\"https://simian.rodeo/tags/FuckCancer\" class=\"mention hashtag\" rel=\"tag\">#<span>FuckCancer</span></a></p>",
  "url": "https://simian.rodeo/@kitchen",
  "manuallyApprovesFollowers": false,
  "discoverable": true,
  "published": "2022-11-06T00:00:00Z",
  "devices": "https://simian.rodeo/users/kitchen/collections/devices",
  "publicKey": {
    "id": "https://simian.rodeo/users/kitchen#main-key",
    "owner": "https://simian.rodeo/users/kitchen",
    "publicKeyPem": "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA3XV62VbZ1P4CfqzbQOpS\n7VWhcZAB8SYVf2Kge4u3z1UBhqXS3VTjlY79enRcND8jAS/Lq/ud/P2lrATyAZqu\n2qRpsnWEPdUuKCBIDmkquXe2VXIW7mBur4buQosTAl6gYEfxVt1Ct7I3LBWgSxb2\n59KigCHE58WO4ZT7Q0fyjnyNrRCo/ifhl041hl/L5Fom5bOqMq8op4yRPXJ579V4\nxRzxG1b7t0NWD3TE1C2aN9qdIUP8rdSw5ljm2uA3VCR5HkCmm892H/nKDF3g2Uy1\np3m+rC/RR5egcPPhJb6kRSBjiExL5sl07KDzGYziQUpUIdGZMXQFQprhTD/sLQsf\n5wIDAQAB\n-----END PUBLIC KEY-----\n"
  },
  "tag": [
    {
      "type": "Hashtag",
      "href": "https://simian.rodeo/tags/fuckcancer",
      "name": "#fuckcancer"
    }
  ],
  "attachment": [
    {
      "type": "PropertyValue",
      "name": "pronouns",
      "value": "he/him"
    },
    {
      "type": "PropertyValue",
      "name": "blog",
      "value": "<a href=\"https://words.kitchen.io/\" target=\"_blank\" rel=\"nofollow noopener noreferrer me\"><span class=\"invisible\">https://</span><span class=\"\">words.kitchen.io/</span><span class=\"invisible\"></span></a>"
    },
    {
      "type": "PropertyValue",
      "name": "speaks",
      "value": "English. Español poquito."
    },
    {
      "type": "PropertyValue",
      "name": "license",
      "value": "<a href=\"https://creativecommons.org/licenses/by-nc/4.0/\" target=\"_blank\" rel=\"nofollow noopener noreferrer me\"><span class=\"invisible\">https://</span><span class=\"ellipsis\">creativecommons.org/licenses/b</span><span class=\"invisible\">y-nc/4.0/</span></a>"
    }
  ],
  "endpoints": {
    "sharedInbox": "https://simian.rodeo/inbox"
  },
  "icon": {
    "type": "Image",
    "mediaType": "image/jpeg",
    "url": "https://media.simian.rodeo/giddyup/accounts/avatars/109/294/272/844/936/789/original/9872552c18acdf40.jpeg"
  },
  "image": {
    "type": "Image",
    "mediaType": "image/jpeg",
    "url": "https://media.simian.rodeo/giddyup/accounts/headers/109/294/272/844/936/789/original/1dfd62d492be4163.jpeg"
  }
}
```

So this is what we'll start with. Turn things like "@kitchen@simian.rodeo" into profiles using webfinger and that. Good start

