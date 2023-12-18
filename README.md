## My Notes
### Layout,
1. One benefit of using layouts in Next.js is that on navigation, only the page components update while the layout won't re-render. This is called partial rendering

### Static Rendering (by default),
1.  There are a couple of benefits of static rendering: Faster Websites and Improve SEO
2.  Static rendering is useful for UI with no data or data that is shared across users, such as a static blog post or a product page. It might not be a good fit for a dashboard that has personalized data that is regularly updated.

### Dynamic Rendering,
1. There are a couple of benefits of dynamic rendering: Real time data and Request time information such as cookies or url search params
2. To use dynamic rendering, use a Next.js API called unstable_noStore inside Server Components or data fetching functions. Example:
```
import { unstable_noStore as noStore } from 'next/cache';
 
export async function fetchRevenue() {
  // Add noStore() here to prevent the response from being cached.
  // This is equivalent to in fetch(..., {cache: 'no-store'}).
  noStore();
 
  // ...
}
```

### Streaming (Loading Indicator),
1. There are two ways you implement streaming in Next.js: At the page level, with the loading.tsx file and For specific components, with <Suspense fallback;>

### Fetch Data,
1. fetching data from the client, you will need an API layer that runs on the server to avoid exposing your database secrets to the client.(u don't need API layer if u on server component)

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

### Random Example
-) Search feature in next js
```
  const searchParams = useSearchParams();

  const { replace } = useRouter();
  const pathname = usePathname();

  function handleSearch(term: string) {
    const params = new URLSearchParams(searchParams);

    if (term) params.set('query', term);
    else params.delete('query');

    replace(`${pathname}?${params}`);
  }
```

-) When to use the useSearchParams() hook vs. the searchParams prop?

Whether you use one or the other depends on whether you're working on the client or the server. use the useSearchParams() hook to access the params from the client. Server Component  fetches its own data, so you can pass the searchParams prop from the page to the component.
<br />
<br />
<br />
