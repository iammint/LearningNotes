# DAY16 Solving the Jump Game by Depth First Search Algorithm
```js
function DFS(n,s,target,seen = new Set()) {
    if (n[s] === target) {
    return true;
    }
    for (const i of [-1, 1]) {
    const next = s + i * n[s];
    if (next >= 0 && next < n.length - 1 && !seen.has(next)) {
        seen.add(next)
        if (DFS(n, next, target, seen)) {
        return true;
        }
        seen.delete(next);
    }
    }
    return false;
}
```