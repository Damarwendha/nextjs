## My Notes
### Layout,
1. One benefit of using layouts in Next.js is that on navigation, only the page components update while the layout won't re-render. This is called partial rendering

## Fetch Data,
1. If you're fetching data from the client, you want to have an API layer that runs on the server to avoid exposing your database secrets to the client.(u don't need API layer if u on server component)

### Font,
1. antialiased (tailwind) classname, benefit font terlihat smooth
2. pakai font dari nextjs, benefit font ringan saat proses rendering di client. example:
```
## app/ui/fonts.ts ##

import { Inter, Lusitana } from 'next/font/google';

// Primary Font
export const inter = Inter({ subsets: ['latin'] });

// Secondary Font
export const lusitana = Lusitana({
  subsets: ['latin'],
  weight: ['400', '700'],
});
```

## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.
