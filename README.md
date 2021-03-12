# cbor-tag-multimap

This document describes a CBOR tag for multimaps encoded as arrays of pairs.

**Tag value**: TBD

**Data item**: Array (major type 4)

**Semantics summary**: Array of key-value pairs where keys may be duplicated.

## Semantics

This tag represents an array of key-value pairs where keys may be duplicated. Each key-value pair is encoded as a two-element subarray of major type 4, size 2 (header byte `0x82`). The keys and values may be of any valid CBOR type and need not be homogenous.

## Rationale

According to [RFC7048, section 2-1](https://tools.ietf.org/html/rfc7049#section-2.1):

> A map that has duplicate keys may be well-formed, but it is not valid, and thus it causes indeterminate decoding

This limitation makes it either impossible or unpractical to encode multimap data structures as CBOR maps (major type 5).

A workaround is to encode multimap data structures as arrays of pairs. This tag allows a CBOR decoder to determine a priori that the following array is indeed an array of pairs and can thus be safely interpreted as a multimap.
