## 사이트 유지보수 가이드

1. **개발 환경 준비**
   - Hugo Extended 최신 버전을 설치하고 `npm install`로 필요한 자산 빌드 도구를 준비합니다.
   - `hugo server -D`로 로컬 미리보기를 띄워 콘텐츠/레이아웃 변경을 즉시 확인합니다.
2. **콘텐츠 업데이트**
   - 새 글·인물·사진 등은 `content/` 하위의 해당 디렉터리에 Markdown 파일로 추가하거나 수정합니다.
   - 공통 설정(메뉴, 파라미터 등)은 `config/_default/*.yaml`에서 관리합니다.
3. **스타일·스크립트 관리**
   - SCSS, JS 등 자산은 `assets/` 디렉터리에서 관리하고, 변경 후 `hugo`가 자동으로 번들링합니다.
4. **빌드 및 배포**
   - 릴리스 전에 `hugo server -D`로 전체 사이트를 점검합니다.
   - Netlify/GitHub Pages 등 배포 파이프라인이 최신 브랜치(`main`)로 트리거되는지 확인합니다.

필요 시 [HugoBlox 문서](https://docs.hugoblox.com/)와 저장소 `README`를 참고해 추가 설정을 적용하세요.

## 주요 섹션별 수정 방법

- **Publications (`content/publication/`)**
   - 각 논문은 개별 디렉터리의 `index.md`로 관리되며 `title`, `authors`, `publication`, `year`, `featured` 등을 front matter에 정의합니다.
   - BibTeX로 가져올 경우 Hugo Blox CLI(구 Academic CLI)를 활용하고, 반영 후 `hugo server -D`로 레이아웃을 확인합니다.
- **People (`content/people/`, `content/admin/authors/`)**
   - `people/index.md`에서 섹션 순서를 제어하고, 구성원별 프로필은 `content/admin/authors/<slug>/index.md`를 수정합니다.
   - 새 멤버 사진은 `static/media/uploads/`에 업로드한 뒤 front matter의 `image` 경로를 맞춰줍니다.
- **Course 개요 (`content/course/_index.md`)**
   - 과목 리스트 제목, 설명, CTA 버튼을 `_index.md` front matter에서 조정합니다.
- **Course 상세 (`content/course/<course>/index.md`)**
   - 강의별 소개, 담당 교수, 자료 링크 등을 front matter와 본문에 추가하고, 필요 시 `resources` 블록으로 슬라이드를 첨부합니다.
- **Research Project (`content/project/`)**
   - 프로젝트별 디렉터리를 만들고 `summary`, `tags`, `featured`, `external_link` 등을 설정합니다.
   - 카드 노출 순서는 `weight`로 제어하거나 `featured: true`로 메인 배너에 올립니다.
- **News (`content/post/`)**
   - 소식 글은 `content/post/<slug>/index.md`에 작성하며 `date`, `categories`, `featured_image`를 지정합니다.
   - 발행 전에는 `draft: true`로 저장하고 검수 후 `false`로 바꿉니다.
- **Photos (`content/photos/`)**
   - 행사·앨범 폴더에 `index.md`와 이미지를 넣고, 사진 파일은 `static/media/uploads/` 또는 해당 폴더에 위치시킵니다.
   - 슬라이드 노출 순서는 front matter의 `gallery` 배열에서 설정합니다.
- **Contact (`content/contact/index.md`)**
   - 주소, 이메일, 지도 좌표 등은 front matter의 `address`, `contact_links`로 관리하며 폼 연동은 `config/_default/params.yaml`의 `contact` 블록을 수정합니다.

모든 섹션 수정 후 `hugo server -D`로 미리 확인하고, git 커밋·푸시 후 배포 파이프라인이 정상 작동하는지 점검하세요.
