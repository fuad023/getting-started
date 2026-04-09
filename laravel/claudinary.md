#### Add the PHP SDK

```
composer require cloudinary/cloudinary_php
```

#### Setup `.env`

```
# CLOUDINARY_KEY=188497841838818
# CLOUDINARY_SECRET=g0PN8ZfcLFNxpCOe9SFE0G9dnIM
# CLOUDINARY_CLOUD_NAME=dbfng8qkq

CLOUDINARY_URL=cloudinary://188497841838818:g0PN8ZfcLFNxpCOe9SFE0G9dnIM@dbfng8qkq
```

#### Create a service `app/Services/CloudinaryService`

```
<?php

namespace App\Services;

use Cloudinary\Cloudinary;

class CloudinaryService
{
    protected Cloudinary $cloudinary;

    public function __construct()
    {
        // $this->cloudinary = new Cloudinary([
        //     'cloud' => [
        //         'cloud_name' => config('services.cloudinary.cloud_name'),
        //         'api_key'    => config('services.cloudinary.api_key'),
        //         'api_secret' => config('services.cloudinary.api_secret'),
        //     ],
        // ]);

        $this->cloudinary = new Cloudinary(config('services.cloudinary.url'));
    }

    public function uploadMany($files, $folder)
    {
        $uploaded = [];
        $failed   = [];

        foreach ($files as $file) {
            try {
                $result = $this->uploadToCloudinary($file, $folder);

                $file_created = $this->storeMetaDataInDatabase($result, $file);

                $uploaded[] = // $file_created;
                [
                    'public_id' => $result['public_id'],
                    'url' => $result['secure_url'],
                ];

            } catch (\Exception $e) {
                $failed[] = [
                    'file'    => $file->getClientOriginalName(),
                    'message' => $e->getMessage(),
                ];
            }
        }

        return [
            'uploaded' => $uploaded,
            'failed'   => $failed
        ];
    }

    private function uploadToCloudinary($file, $folder = 'uploads') {
        return $this->cloudinary->uploadApi()->upload(
            $file->getRealPath(),
            [
                'folder' => $folder,
                'resource_type' => 'auto'
            ]
        );
    }

    private function storeMetaDataInDatabase($result, $file) {
        // return File::create([
        //     'original_name' => $file->getClientOriginalName(),
        //     'public_id'     => $result['public_id'],
        //     'url'           => $result['secure_url'],
        //     'size'          => $result['bytes'],
        //     'type'          => $result['resource_type'],
        //     'mime_type'     => $file->getMimeType(),
        // ]);
    }

    public function delete($publicId)
    {
        return $this->cloudinary->uploadApi()->destroy($publicId);
    }
}
```

#### Add the following in `config/services.php`

```
'cloudinary' => [
    // 'key'        => env('CLOUDINARY_KEY'),
    // 'secret'     => env('CLOUDINARY_SECRET'),
    // 'cloud_name' => env('CLOUDINARY_CLOUD_NAME'),

    'url' => env('CLOUDINARY_URL'),
],
```

#### Use in routes/controllers

```
<?php

use App\Services\CloudinaryService;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Route;

Route::post('/uploads', function (Request $request, CloudinaryService $cloudinary) {
    $request->validate([
        'files'       => 'required|array|max:10',  // limit to 10 files at once
        'files.*'     => 'required|file|max:51200' // 50MB per media
    ]);

    $results = $cloudinary->uploadMany($request->file('files', []), 'new_uploads');

    return response()->json($results);
});
```

