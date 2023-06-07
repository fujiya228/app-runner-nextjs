# App Runnerにデプロイする

参考: [Next.jsのスタンドアロンモードでビルドしたイメージを AWS App Runnerへデプロイする](https://dev.classmethod.jp/articles/app-runner-nextjs/)

2023/06/08 現在

修正が必要だった
1. standaloneモードの書き方
2. 13.4.4 => 13.3.4（package.jsonを書き換えてインストールしなおしただけ）
3. experimental.appDir: true の追加

### 補足&注意

- standaloneモードは書き方が変わるらしい。警告でてた。
    ```
    - warn Invalid next.config.js options detected: 
    - warn     The value at .experimental has an unexpected property, outputStandalone, which is not in the list of allowed properties (appDocumentPreloading, adjustFontFallbacks, adjustFontFallbacksWithSizeAdjust, allowedRevalidateHeaderKeys, amp, clientRouterFilter, clientRouterFilterRedirects, clientRouterFilterAllowedRate, cpus, memoryBasedWorkersCount, craCompat, disableOptimizedLoading, disablePostcssPresetEnv, esmExternals, appDir, serverActions, extensionAlias, externalDir, externalMiddlewareRewritesResolve, fallbackNodePolyfills, fetchCacheKeyPrefix, forceSwcTransforms, fullySpecified, gzipSize, incrementalCacheHandlerPath, isrFlushToDisk, isrMemoryCacheSize, largePageDataBytes, legacyBrowsers, manualClientBasePath, middlewarePrefetch, newNextLinkBehavior, nextScriptWorkers, optimizeCss, optimisticClientCache, outputFileTracingRoot, outputFileTracingExcludes, outputFileTracingIgnores, outputFileTracingIncludes, pageEnv, proxyTimeout, serverComponentsExternalPackages, scrollRestoration, sharedPool, sri, strictNextHead, swcFileReading, swcMinify, swcPlugins, swcTraceProfiling, urlImports, workerThreads, webVitalsAttribution, mdxRs, typedRoutes, webpackBuildWorker, turbo, instrumentationHook, turbotrace, logging).
    - warn See more info here: https://nextjs.org/docs/messages/invalid-next-config
    - warn You have enabled experimental feature (outputStandalone) in next.config.js.
    - warn Experimental features are not covered by semver, and may cause unexpected or broken application behavior. Use at your own risk.

    - warn experimental.outputStandalone has been renamed to "output: 'standalone'", please move the config.
    ```
  - 指示通り対応
  ```
  const nextConfig = {
    reactStrictMode: true,
    output: 'standalone',
  };
  ```
- コピーするファイルの考え方
  - `public` と `.next/static` は自動では`standalon`フォルダへ入らないようだ。これらのフォルダはCDNにアップすることが期待されているから、らしい。
  - [参考](https://zenn.dev/waddy/scraps/2149377ee12a3b)
- 13.4.4はダメらしい（[参考](https://qiita.com/Kanahiro/items/aaec2ddf5ffefecbbc31)）
  - 13.3.4に落として解決
  - ビルド時、configに`experimental.appDir: true`が必要

<details>
<summary>History</summary>
<br/>

Comming soon...

</details>

<details>
<summary>Next.js</summary>
<br/>


# Next.js

This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/basic-features/font-optimization) to automatically optimize and load Inter, a custom Google Font.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.


</details>
