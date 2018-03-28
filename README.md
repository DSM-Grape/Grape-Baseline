# Grape-Baseline
## JSON Schema
```
{
    "baseURL": "grape.io",
    "basePath": "/",

    "info": {
        "title": "Grape : API documentation platform",
        "decsription": "API 문서화 플랫폼인 Grape에 대한 API 문서입니다.",
        "version": "0.1-beta"
    },

    "groups": {
        "게시글": "게시글 관련 API들",
        "계정" : "계정 관련 API들"
    },

    "advices": {
        "401": {
            "description": "JWT Access token이 없음"
        },
        "403": {
            "description": "권한 없음"
        },
        "404": {
            "description": "페이지 없음"
        },
        "406": {
            "description": "처리할 수 없는 Content-Type"
        }
    },

    "properties": {
        "jwtheader": "hjaahsbdjehab.adbhjebadhbaedbad.beahdbaedhbaedeadbkh"
    },

    "schemes": {
        "PostSchema": {
            "id": {
                "type": "str",
                "required": true,
                "exampleValue": "a1a1a1"
            },
            "category": {
                "type": "str",
                "description": "목록을 불러올 게시글의 카테고리",
                "required": true,
                "exceptions": [
                    "존재하지 않는 카테고리라면 기본값으로 처리됩니다."
                ],
                "default": "life",
                "exampleValue": "love"
            },
            "title": {
                "type": "str",
                "description": "게시글의 제목",
                "required": true,
                "exampleValue": "제목입니다"
            },
            "content": {
                "type": "str",
                "description": "게시글의 내용",
                "required": true,
                "exampleValue": "내용입니다"
            }
        }
    },

    "resource": {
        "/post": {
            "description": "",
            "group": "게시글",
            "methods": {
                "get": {
                    "description": "게시글 목록 불러오기",
                    "headers": {
                        "Authorization": {
                            "required": true,
                            "exampleValue": "JWT #jwtheader"
                        }
                    },
                    "params": {
                        "_schema": {
                            "name": "PostSchema",
                            "exclude": ["id", "title", "content"]
                        },
                        "page": {
                            "required": false,
                            "type": "int",
                            "description": "조회할 페이지",
                            "exceptions": [
                                "파라미터가 전달되지 않으면 기본값으로 처리됩니다.",
                                "최대 페이지를 넘어가면 기본값으로 처리됩니다."
                            ],
                            "default": 1
                        }
                    },
                    "response": {
                        "200": {
                            "description": "게시글 조회 성공",
                            "examples": {
                                "application/json": {
                                    "contentLength": 15,
                                    "items": [
                                        {
                                            "_schema": {
                                                "name": "PostSchema",
                                                "exclude": ["content", "category"]
                                            }
                                        },
                                        {
                                            "_schema": {
                                                "name": "PostSchema",
                                                "exclude": ["content", "category"]
                                            }
                                        }
                                    ]
                                },
                                "text/plain": "Hello World"
                            }
                        },
                        "204": {
                            "description": "게시글 없음"
                        },
                        "401": "#401"
                    }
                },
                "post": {
                    "description": "게시글 작성",
                    "params": {},
                    "body": {
                        "application/x-www-form-urlencoded": {
                            "_schema": {
                                "name": "PostSchema",
                                "exclude": ["id"]
                            }
                        },
                        "application/json": {
                            "_schema": {
                                "name": "PostSchema",
                                "exclude": ["id"]
                            }
                        }
                    },
                    "response": {
                        "201": {
                            "description": "게시글 작성 성공"
                        },
                        "_advices": ["401", "403", "406"]
                    }
                }
            }
        }
    }
}
```
