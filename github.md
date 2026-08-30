# GitHub

## Report Actions artifact storage

```bash
printf "%-55s %12s %12s\n" "REPOSITORY" "ARTIFACT MB" "CACHE MB"
printf "%-55s %12s %12s\n" "----------" "-----------" "--------"

gh repo list gibbok --limit 1000 --json nameWithOwner -q '.[].nameWithOwner' |
while read repo; do

  artifacts=$(gh api --paginate "/repos/$repo/actions/artifacts?per_page=100" \
    --jq '[.artifacts[] | select(.expired == false) | .size_in_bytes] | add // 0' \
    2>/dev/null)

  cache=$(gh api "/repos/$repo/actions/cache/usage" \
    --jq '.active_caches_size_in_bytes // 0' \
    2>/dev/null)

  artifacts=${artifacts:-0}
  cache=${cache:-0}

  if [ "$artifacts" -gt 0 ] || [ "$cache" -gt 0 ]; then
    printf "%-55s %12.2f %12.2f\n" \
      "$repo" \
      "$(awk "BEGIN {print $artifacts/1024/1024}")" \
      "$(awk "BEGIN {print $cache/1024/1024}")"
  fi
done
```
