# ts-inferredProject1

Steps to reproduce:

`git clone git@github.com:brieb/ts-inferredProject1.git`

`cd ts-inferredProject1`

`yarn`

`code .`

Open `projects/proj-03/proj03.ts`.

Observe that the `import { proj02 } from ":proj-02/proj02";` import resolves as expected.

Create new file `projects/proj-03/foo.ts` with the following contents:

```typescript
import { proj02 } from ":proj-02/proj02";

export function foo() {
  proj02();
}
```

Notice the error under `":proj-02/proj02"`:

```
Cannot find module ':proj-02/proj02' or its corresponding type declarations.ts(2307)
```

Run "TypeScript: Open TS Server log" from the command palette.

Notice that our new file belongs to `/dev/null/inferredProject1*` rather than `projects/proj-03/tsconfig.json` (which was correctly determined for the pre-existing `projects/proj-03/proj03.ts` we opened first).

Here is a gist containing an example of such a tsserver.log: https://gist.github.com/brieb/0f58249bfdb76c3679041e93c3ea8c3c

In particular, https://gist.github.com/brieb/0f58249bfdb76c3679041e93c3ea8c3c#file-tsserver-log-L305-L309
```
Info 136  [17:25:15.493] Open files: 
Info 136  [17:25:15.493] 	FileName: .../repos/ts-inferredProject1/projects/proj-03/proj03.ts ProjectRootPath: .../repos/ts-inferredProject1
Info 136  [17:25:15.493] 		Projects: .../repos/ts-inferredProject1/projects/proj-03/tsconfig.json
Info 136  [17:25:15.493] 	FileName: .../repos/ts-inferredProject1/projects/proj-03/foo.ts ProjectRootPath: .../repos/ts-inferredProject1
Info 136  [17:25:15.493] 		Projects: /dev/null/inferredProject1*
```

Run "TypeScript: Restart TS server" from the command palette.

Notice that the error we were seeing in `projects/proj-03/foo.ts` is no longer present, and the import resolves as expected.
