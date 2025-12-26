Konteksnya pt keen optima solution ingin membuat proposal teknis untuk diajukan ke ke pihak bbws citanduy dengan tujuan untuk mengintegrasikan sistem smopi dengan command center yang sudah ada dan meremake website smopi yang sudah ada, requirement nya dan tantangan sudah saya buat pada file requirement cc-smopi.md \dan pada file tantangan-yang ada.md, tolong buatkan proposal teknis seperti pada file technical kti contoh.pdf dengan menggunakan file requirement dan tantangan tersebut sebagai sumber data. sekarang itu command center sudah memiliki sistem bigboard dan dashboardnya, namun itu belum terintegrasi dengan smopi, jadi ada data yang masih berbeda contohnya data debit kebutuhan air,  aplikasi tersebut akan dibuat dalam bentuk website dan waktu pengerjaan nya itu satu bulan, dan kita akan menggunakan next js dan untuk peta kita akan menggunakan package yg digunakan oleh aplikasi siger dibawah ini:

{
"name": "siger",
"version": "0.1.0",
"private": true,
"scripts": {
"dev": "next dev --turbo",
"build": "next build",
"start": "next start",
"lint": "next lint",
"type-check": "tsc --noEmit",
"db:seed": "tsx prisma/seed.ts",
"db:push": "npx prisma db push",
"db:reset": "npx prisma generate && npx prisma db push --force-reset && npm run db:seed && npx prisma db execute --file prisma/enable-postgis.sql --schema prisma/schema.prisma",
"db:fresh": "npm run db:reset",
"db:reset2": "npx prisma generate && npx prisma db push --force-reset && npx prisma db execute --file prisma/enable-postgis.sql --schema prisma/schema.prisma"
},
"prisma": {
"seed": "tsx prisma/seed.ts"
},
"dependencies": {
"@auth/prisma-adapter": "^2.10.0",
"@copilotkit/react-core": "^1.9.3",
"@copilotkit/react-textarea": "^1.9.3",
"@copilotkit/react-ui": "^1.9.3",
"@copilotkit/runtime": "^1.9.3",
"@heroicons/react": "^2.0.0",
"@hookform/resolvers": "^5.2.1",
"@observablehq/plot": "^0.6.0",
"@prisma/client": "6.15.0",
"@radix-ui/react-accordion": "^1.2.12",
"@radix-ui/react-alert-dialog": "^1.1.15",
"@radix-ui/react-avatar": "^1.1.10",
"@radix-ui/react-checkbox": "^1.3.3",
"@radix-ui/react-dialog": "^1.1.15",
"@radix-ui/react-dropdown-menu": "^2.1.16",
"@radix-ui/react-hover-card": "^1.1.15",
"@radix-ui/react-popover": "^1.1.15",
"@radix-ui/react-progress": "^1.1.7",
"@radix-ui/react-select": "^2.2.6",
"@radix-ui/react-slot": "^1.2.3",
"@radix-ui/react-tabs": "^1.1.13",
"@tanstack/react-query": "^5.85.9",
"@tanstack/react-query-devtools": "^5.85.9",
"@turf/turf": "^6.5.0",
"@types/bcryptjs": "^2.4.6",
"@types/jsonwebtoken": "^9.0.10",
"@types/minio": "^7.1.0",
"@types/node": "^20.0.0",
"@types/react": "^18.2.0",
"@types/react-dom": "^18.2.0",
"@types/xlsx": "^0.0.35",
"@vis.gl/react-google-maps": "^1.5.5",
"adm-zip": "^0.5.16",
"autoprefixer": "^10.4.0",
"bcryptjs": "^3.0.2",
"chart.js": "^4.4.0",
"class-variance-authority": "^0.7.0",
"clsx": "^2.0.0",
"cmdk": "^1.1.1",
"compression": "^1.7.0",
"cors": "^2.8.0",
"d3": "^7.8.0",
"date-fns": "^4.1.0",
"exceljs": "^4.4.0",
"express": "^4.18.0",
"express-rate-limit": "^7.1.0",
"express-validator": "^7.0.0",
"framer-motion": "^11.0.0",
"helmet": "^7.1.0",
"jsonwebtoken": "^9.0.2",
"lottie-react": "^2.4.0",
"lucide-react": "^0.400.0",
"minio": "^8.0.5",
"next": "^15.0.0",
"next-auth": "^5.0.0-beta.29",
"next-pwa": "^5.6.0",
"postcss": "^8.4.0",
"prisma": "6.15.0",
"react": "^18.2.0",
"react-chartjs-2": "^5.2.0",
"react-dom": "^18.2.0",
"react-hook-form": "^7.62.0",
"recharts": "^3.1.2",
"sonner": "^2.0.7",
"tailwind-merge": "^2.0.0",
"tailwindcss": "^3.4.0",
"tailwindcss-animate": "^1.0.7",
"typescript": "^5.6.0",
"workbox-webpack-plugin": "^7.0.0",
"xlsx": "^0.18.5",
"xmldom": "^0.6.0",
"zod": "^3.22.0",
"zustand": "^5.0.8"
},
"devDependencies": {
"@types/adm-zip": "^0.5.7",
"@types/compression": "^1.7.0",
"@types/cors": "^2.8.0",
"@types/d3": "^7.4.0",
"@types/express": "^4.17.0",
"@types/geojson": "^7946.0.16",
"@types/node-fetch": "^2.6.13",
"@types/xmldom": "^0.1.34",
"@typescript-eslint/eslint-plugin": "^6.0.0",
"@typescript-eslint/parser": "^6.0.0",
"eslint": "^8.57.0",
"eslint-config-next": "^15.0.0",
"form-data": "^4.0.4",
"node-fetch": "^2.7.0",
"prettier": "^3.0.0",
"prettier-plugin-tailwindcss": "^0.5.0",
"tsx": "^4.20.5"
},
"engines": {
"node": ">=20.0.0"
}
}

catatan tambahan:
-sistem untuk untuk telemetri nya sudah ada pada sistem command center hanya perlu diseuaikan
-tolong gunakan data dari file fungsional requirement banyak dan mendetail, Semua poin fungsional dimasukkan lengkap
-tolong pastikan lagi semuanya benar seusai dengan file requirementnya, jika ada yang tidak masuk akal tolong beri tahu saya
-tambahkan diagram arsitektur sederhana

tolong tambahkan dan sesuaikan degan hal dibawah ini pada file proposal-teknis-cc-smopi.md dan juga pada file requirement cc-smopi.md:

+ mobile apps (pake Progressive Web App (PWA))
+ integrasi dengan aplikasi forecasting ketersediaan (HIGERTECH)
+ integrasi dengan dashboard manganti (OPSHI)

untuk kedua integrasi tersebut itu, kami tim keenos yg akan mengubah source code mereka dari
sebelumnya mereka menggunakan data dari SMOPI lama menggunakan data dari smopi yang baru akan dibuat ini
 



