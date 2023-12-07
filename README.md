## My Notes
-) **Font**, antialiased (tailwind) classname agar font terlihat smooth & pakai font dari nextjs agar font ringan saat proses rendering di client. example:
```
## app/ui/fonts.ts ##

import { Inter, Lusitana } from 'next/font/google';

export const inter = Inter({ subsets: ['latin'] });
export const lusitana = Lusitana({
  subsets: ['latin'],
  weight: ['400', '700'],
});
```


## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.
